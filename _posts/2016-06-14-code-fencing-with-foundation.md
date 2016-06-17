---
layout:     post
title:     "Code Fencing with Foundation"
subtitle:     ""
categories:   ""
date:       2016-06-14
author:     "Topher"
---
This website is generated using [Jekyll](https://jekyllrb.com/) with a theme that utilizes [Foundation](http://foundation.zurb.com/) for styling. I like Foundation as a framework, but its styling for code blocks isn't really what I want for a code-heavy site.

<img src="{{site.url}}/images/foundation/start.png"/>

Pretty ugly! Each individual line has a border, and no shared background color. Also, obviously, no syntax highlighting. 

The first thing to do is to bring in a copy of `syntax.css`. 

{% highlight css %}
.highlight pre, pre, .highlight .hll { background-color: #f8f8f8; border: 1px solid #ccc; padding: 6px 10px; border-radius: 3px; }
.highlight .c { color: #999988; font-style: italic; }
.highlight .err { color: #a61717; background-color: #e3d2d2; }
.highlight .k { font-weight: bold; }
.highlight .o { font-weight: bold; }
.highlight .cm { color: #999988; font-style: italic; }
.highlight .cp { color: #999999; font-weight: bold; }
.highlight .c1 { color: #999988; font-style: italic; }
.highlight .cs { color: #999999; font-weight: bold; font-style: italic; }
.highlight .gd { color: #000000; background-color: #ffdddd; }
.highlight .gd .x { color: #000000; background-color: #ffaaaa; }
.highlight .ge { font-style: italic; }
.highlight .gr { color: #aa0000; }
.highlight .gh { color: #999999; }
.highlight .gi { color: #000000; background-color: #ddffdd; }
.highlight .gi .x { color: #000000; background-color: #aaffaa; }
.highlight .go { color: #888888; }
.highlight .gp { color: #555555; }
.highlight .gs { font-weight: bold; }
.highlight .gu { color: #800080; font-weight: bold; }
.highlight .gt { color: #aa0000; }
.highlight .kc { font-weight: bold; }
.highlight .kd { font-weight: bold; }
.highlight .kn { font-weight: bold; }
.highlight .kp { font-weight: bold; }
.highlight .kr { font-weight: bold; }
.highlight .kt { color: #445588; font-weight: bold; }
.highlight .m { color: #009999; }
.highlight .s { color: #dd1144; }
.highlight .n { color: #333333; }
.highlight .na { color: teal; }
.highlight .nb { color: #0086b3; }
.highlight .nc { color: #445588; font-weight: bold; }
.highlight .no { color: teal; }
.highlight .ni { color: purple; }
.highlight .ne { color: #990000; font-weight: bold; }
.highlight .nf { color: #990000; font-weight: bold; }
.highlight .nn { color: #555555; }
.highlight .nt { color: navy; }
.highlight .nv { color: teal; }
.highlight .ow { font-weight: bold; }
.highlight .w { color: #bbbbbb; }
.highlight .mf { color: #009999; }
.highlight .mh { color: #009999; }
.highlight .mi { color: #009999; }
.highlight .mo { color: #009999; }
.highlight .sb { color: #dd1144; }
.highlight .sc { color: #dd1144; }
.highlight .sd { color: #dd1144; }
.highlight .s2 { color: #dd1144; }
.highlight .se { color: #dd1144; }
.highlight .sh { color: #dd1144; }
.highlight .si { color: #dd1144; }
.highlight .sx { color: #dd1144; }
.highlight .sr { color: #009926; }
.highlight .s1 { color: #dd1144; }
.highlight .ss { color: #990073; }
.highlight .bp { color: #999999; }
.highlight .vc { color: teal; }
.highlight .vg { color: teal; }
.highlight .vi { color: teal; }
.highlight .il { color: #009999; }
.highlight .gc { color: #999; background-color: #EAF2F5; }
{% endhighlight %}

We'll need to add that into `_includes\head.html`, or wherever your stylesheets are being injected into your site. Be sure to add it after the line that loads Foundation, though.

{% highlight javascript %}
<link rel="stylesheet" href="{{ "/css/foundation.css" | prepend: site.baseurl }}">
<link rel="stylesheet" href="{{ "/css/syntax.css" | prepend: site.baseurl }}">
{% endhighlight %}

Here's what the code highlighting looks like now.
<img src="{{site.url}}/images/foundation/second.png"/>

This looks much better, but still not perfect. Those lines above and below are still coming from the Foundation `foundation.css` stylesheet. I'm going to add my own "code" style to the `syntax.css` to override that.

{% highlight css %}
code {
  font-family: Consolas, "Liberation Mono", Courier, monospace;
  font-weight: normal;
  color: #333333;
  border-style: none;
}
{% endhighlight %}

Much better!
<img src="{{site.url}}/images/foundation/final.png"/>
