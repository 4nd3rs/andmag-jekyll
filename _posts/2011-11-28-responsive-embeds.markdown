---
author: admin
comments: true
date: 2011-11-28 21:49:34+00:00
layout: post
slug: responsive-embeds
title: Responsive embeds
wordpress_id: 127
categories:
- Responsive Web Design
- Video
tags:
- A List Apart
- Flexible video
- Responsive video
- RWD
- Slideshare
- Video
- Vimeo
- YouTube
---

This article shows examples of how to embed video and other iframes in a responsive web design and has examples with YouTube, Vimeo and Slideshare.
<!-- more -->
I found a neat little CSS trick on the A List Apart article "[Creating Intrinsic Ratios for Video](http://www.alistapart.com/articles/creating-intrinsic-ratios-for-video/)" and I did some experimenting with it. (Yes, I had to look up the word [Intrinsic](http://en.wikipedia.org/wiki/Intrinsic_and_extrinsic_properties)...)

The problem with embed code that you copy from websites like YouTube is that they often contain a fixed width and height in pixels. And that does not work too well in responsive designs. In a responsive design we have a container with a relative width and we want the embedded object to be relative to our container. This is not possible with all embeds as some of them insist on having a fixed width. If you encounter such embeds, the workaround is probably to move some of the code to the server side or javascript and set the width to the pixel value that you think is most appropriate. It will work, but it will not be flexible like the method shown here.

This technique is fully flexible and I have tests below with Vimeo, SlideShare and YouTube (sorry if this post took long to load...). Here are the steps to make it work.

First, you just need to remove the width/hight attributes from the embed code you get:

[code]
<!-- original -->
<iframe 
src="http://player.vimeo.com/video/32071937?title=0&amp;byline=0&amp;portrait=0" 
width="400" 
height="225" 
frameborder="0"
 webkitAllowFullScreen mozallowfullscreen allowFullScreen>
</iframe>

<!-- removed width/height -->
<iframe 
src="http://player.vimeo.com/video/32071937?title=0&amp;byline=0&amp;portrait=0" 
frameborder="0" 
webkitAllowFullScreen mozallowfullscreen allowFullScreen>
</iframe>
[/code]

Next step is to wrap this in a container tag so that we can style it:

[code]
<div class="embed-container">
    <!-- embed code goes here-->
</div>
[/code]

Then comes the CSS. First, we style the container:

[code]
.embed-container {
	position: relative;
	padding-bottom: 56.25%; /* 16/9 ratio */
	padding-top: 30px; /* IE6 workaround*/
	height: 0;
	overflow: hidden;
}
[/code]

I'm not going to explain all this in detail, the [original article](http://www.alistapart.com/articles/creating-intrinsic-ratios-for-video/) does that better than I can anyway, but this code asumes a 16/9 ratio (56,25%) on the embed. Next step is to style the actual embed. Some embeds serve iframe, object or embed, based on device so we style all three:

[code]
.embed-container iframe,
.embed-container object,
.embed-container embed {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
[/code]



That's it. Here are some examples:





## Vimeo example





   



[code]
<div class="embed-container">
   <iframe 
      src="http://player.vimeo.com/video/22669590?title=0&amp;byline=0&amp;portrait=0" 
      frameborder="0" 
      webkitAllowFullScreen mozallowfullscreen allowFullScreen>
   </iframe>
</div>
[/code]



## Youtube example





   



[code]
<div class="embed-container">
   <iframe 
      src="http://www.youtube.com/embed/TFWDUsvLCoE" 
      frameborder="0">
   </iframe>
</div>
[/code]



## Slideshare example










[code]
<div class="embed-container">
   <iframe 
      src="http://www.slideshare.net/slideshow/embed_code/1488558" 
      frameborder="0" 
      marginwidth="0" 
      marginheight="0" 
      scrolling="no">
   </iframe>
</div>
[/code]



PS. There is a jQuery plugin that does the work for you called [FitVids.js](http://fitvidsjs.com/), but this is so simple and works without JavaScript, so I do not see why we should bring on a JS library in order to get it to work.





UDPATE: I have tested the technique on a few mobile devices, and the technique works good, but the content inside the embed does not work too good... Read more [here](http://amobil.se/2011/12/responsive-embeds-device-testing/)





UPDATE 2: I have created a fallback solution for devices that does not support the embed by using server side techniques: [Responsive embeds + RESS](http://amobil.se/2012/01/responsive-embeds-ress/)
