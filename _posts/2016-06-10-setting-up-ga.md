---
layout:     post
title:     "Setting up Google Analytics"
subtitle:     "For the complete beginner"
categories:   "martech google_analytics"
date:       2016-06-10
author:     "Topher"
---
<h4>Measuring and Analyzing Traffic</h4>
One mantra about startups is “don’t start with a solution, start with a problem that needs to be solved.” While that's really more about finding your market, I want to talk about **my** problem, and figure out the solution.

I’m part of a team starting a new venture, and we want to know exactly what it is we should be doing. We need data in order to make the right decisions. Particularly, we need to know about the market, and what is resonating with people and what doesn’t resonate with people.

(Wow, it all just crystalized to me how much of the “Lean Startup” is actually about market, and marketing!)

Back to **my** problem, and my pain point I’m trying to address.

We’re in the discovery phase of this endeavor. We have some thoughts and plans as to how we can bring value to people. But we don’t know yet exactly what will resonate with the market — or even who the market is!

As of today, a few people will stumble through the site, clicking a link or two that I’ve scattered around on some of my personal things like [LinkedIn](https://www.linkedin.com/in/tophermarie) and [Twitter](https://twitter.com/topher_marie). We haven’t built the page into anything yet, it's basically just a placeholder. You might call it minimal viable product? At least in terms of “it’s a website, and it’s **possible** for people to view it and to ask us to contact them.” We know we need to start building our brand and our identity, and frankly we’re discovering that as we go.

Enter the Build-Measure-Learn lifecycle. What we want to do is to measure who is coming to the site and see what they’re doing. We can then iterate and experiment on that information.

A little googling -- I wasn’t kidding when I said I was new to this stuff -- tells me that  most commonly used tool for “web analytics" is Google Analytics. I do see talk of competitors, but Google Analytics is free and fairly well respected. It’s also what the marketing department used at my previous startup. (Of course, I am using Google, and Google is recommending Google. It’s turtles all the way down.)

Let's give it a shot and see how it works.



<h4>Signing up is easy. </h4>

This is me visiting [http://www.google.com/analytics](http://www.google.com/analytics).
<br/>
<img src="{{site.url}}/images/ga-start.png"/>

<h4>Setting up the new account is easy too</h4>
<img style="max-width: 600px; height: auto;" src="{{site.url}}/images/ga-signup-full.png"/>

<h4>Get the tracking ID</h4>
And... I'm in. The key here is that I've been granted a **Tracking ID** that Google Analytics will use to, well, *track* the activity on my website for me. They even provide the JavaScript necessary to make this happen.

If there's one thing I think Google is very good at, it's tracking people. 

<img style="max-width: 600px; height: auto;" src="{{site.url}}/images/ga-main.png"/>

<h4>Google Analytics Tracking ID with Jekyll</h4>
Next step, I need to get that tracking number to be sent to Google Analytics on every page load. 

Since this site is generated via Jekyll, it's pretty simple for me to have it included on every page. I created a file in the includes directory with the JavaScript above.

`_includes\analytics.js`
{% highlight javascript %}
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
  })(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-79225112-1', 'auto');
  ga('send', 'pageview');

</script>
{% endhighlight %}

It's ok for me to share this, there's nothing secret in here. If you open up the source of this webpage, you're able to see that code. 

The next part is just making sure it gets included on each page in my Jekyll site so that Google Analytics will be able to track activity. I added the following line to what was already there...

`_includes\head.js`
{% highlight liquid %}
{% raw %}
{% include analytics.html %}
{% endraw %}
{% endhighlight %}

...and voila, tracking is set up! 

Here's my dashboard after a few days of sitting. Not very impressive. Most of those visits are from me testing and configuring the website. Ha, well, I did say I was going to be open about this process, and the site is still new.

<img style="max-width: 600px; height: auto;" src="{{site.url}}/images/ga-dashboard.png"/>

Next exploration -- how to analyze what's going on in Google Analytics (for the complete beginner).
