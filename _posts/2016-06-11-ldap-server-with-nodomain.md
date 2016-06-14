---
layout:     post
title:     "New LDAP server getting 'nodomain' as suffix"
subtitle:     "Solving the mystery of the inconsistent rootDN"
categories:   "identity"
date:       2016-06-11
author:     "Topher"
---
**A few days ago we had occasion to spin up a new LDAP server.** 

One of our backend servers filled its disk (through negligent logging). Since the process to build new ones is 'puppetized', I thought it would be easiest just to build an equivalent server and have it take over the role. I'd done this a few weeks back, and it came up flawlessly. I was pretty confident.

**Hubris comes before a fall.** Or something like that. The LDAP service on the newly created machine came up 'different'. Like the cat from [Pet Sematary](http://www.imdb.com/title/tt0098084/). Just not right.

Specifically, the puppet script choked when it tried to apply an "ldif" with a password for my admin user.

{% highlight bash %}
/usr/bin/ldapadd -D "cn=admin,dc=rogueidentity,dc=com" -w "somepassword" -f /etc/ldap/schema/newschema.ldif
ldap_bind: Invalid Credentials (49).
{% endhighlight %}

My first reaction was that it must have the wrong password. But no, it was correct and worked on all the other servers that had spun up in the past.

After some investigation, I noticed that my database had unexpected entries. 

{% highlight bash %}
olcSuffix: dc=nodomain
olcRootDN: cn=admin,dc=nodomain
{% endhighlight %}

I would have expected this to be
{% highlight bash %}
olcSuffix: dc=rogueidentity,dc=com
olcRootDN: cn=admin,dc=rogueidentity,dc=com
{% endhighlight %}

The subsequent ldif files depend on that fact, actually, in that they do modifies and deletes based on that string. 
The question is, what was now (unexpectedly) missing that was putting **nodomain** in there instead of **dc=rogueidentity,dc=com**?

I had an old manual script to check against. I pared down that script to walk through each step so I could see where the rogueidentity domain was being added. 

What was bizarre is that there's no text anywhere that would exactly match that. I've grepped through each ldif, each script, every puppet manifest, and there's just nothing there for **dc=rogueidentity,dc=com**. 

It must be coming from outside the scripts!

After stripping down to the very first steps of even installing the **slapd** service, I found the issue. The raw installation will have an organization based on the domain of the server. In this particular case I had not given the server a name in **/etc/hosts**, so it used a default name -- **nodomain** -- for the suffix.

The solution then is simple. Have puppet modify the **/etc/hosts** file appropriately, so it's something like

{% highlight bash %}
10.20.1.1 ldap-provider.rogueidentity.com ldap-provider
10.20.1.101 puppet-master
{% endhighlight %}

**Success!** The next attempt to spin up the server worked perfectly. 
{% highlight bash %}
olcSuffix: dc=rogueidentity,dc=com
olcRootDN: cn=admin,dc=rogueidentity,dc=com
{% endhighlight %}

Lesson learned -- make sure you have your domain configured in **/etc/hosts** in order to have it applied correctly by **slapd**.

