---
layout:     post
title:     "Views and Filtering in Google Analytics"
subtitle:     ""
categories:   "google_analytics"
date:       2016-06-17
author:     "Topher"
---
I'm getting started with Google Analytics (and "lean analytics" in general). [Here]({% post_url 2016-06-10-setting-up-ga %}) is the previous post, in which I basically just enroll my site in the program. This time, I'm wanting to start looking at the data being gathered. 

I've seen it recommended several [places](http://larslofgren.com/analytics/the-3-profiles-that-every-google-analytics-account-needs) that you create a few separate "views" of your Google Analytics data. The first of these I'm calling "All Web Site Data", the second "Primary", and the final "Test." The rational here is that "All Web Site Data" doesn't do any customization or filtering, that "Primary" be the one that you usually use, and that "Test" is available to try out any new customizations before inflicting it upon your site. Any data that is lost due to bad filtering or logic is just gone, and having a few layers of test and redundancy is healthy.

Creating your new view is easy. Under 'Admin', in the 'Views' column select the drop down list and choose "Create new view."
<div class="row">
  <div class="small-8 large-8 columns">
<img src="{{site.url}}/images/ga/new-view.png" border="1"/>
  </div>
</div>

Set the name of the view.
<div class="row">
  <div class="small-8 large-8 columns">
<img src="{{site.url}}/images/ga/name-view.png" border="1"/>
  </div>
</div>

Next, I want to add a filter to remove all of the visits from my home IP address. For a bigger company this might not be a big deal as those visits will get lost in the noise. For me, right now? That's the majority of the traffic.

In the 'Views' column select 'Filters' and then '+Add Filter.'
<div class="row">
  <div class="small-8 large-8 columns">
<img src="{{site.url}}/images/ga/filter.png" border="1"/>
  </div>
</div>

The other thing I want to do is to set up a preliminary 'Goal' to start assessing how people are using my site. A goal is an indication of “hey, the person on the site did something that I like!”

The first and most obvious goal I set up is the conversion — someone has decided they want to contact us and goes to the contact us page.

(Note that that's not **really** success in our case, but let’s just knock out this iteration and then we can revise later if we’re not seeing what we expect.)

From the 'Views' column select 'Goals' and then '+Add Goal.'

Choose the template.
<div class="row">
  <div class="small-8 large-8 columns">
    <img src="{{site.url}}/images/ga/goal1.png" border="1"/>
  </div>
</div>
<br/>
Set the type as 'Destination.'
<div class="row">
  <div class="small-8 large-8 columns">
    <img src="{{site.url}}/images/ga/goal2.png" border="1"/>
  </div>
</div>
<br/>
So long as they hit the 'contact.html' page, I'm happy for now.
<div class="row">
  <div class="small-8 large-8 columns">
    <img src="{{site.url}}/images/ga/goal3.jpg" border="1"/>
  </div>
</div>
<br/>
Now with a new view, a filter to remove my own website hits, and a goal of getting people to the contact page, let's let this stew a few days and see what data turns up.
