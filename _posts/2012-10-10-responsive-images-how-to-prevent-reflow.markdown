---
author: admin
comments: true
date: 2012-10-10 21:04:42+00:00
layout: post
slug: responsive-images-how-to-prevent-reflow
title: Responsive images - how to prevent reflow
wordpress_id: 369
categories:
- Responsive Images
- Responsive Web Design
tags:
- browser reflow
- flexibale images
- reflow
- responsive images
---


This is what we have been taught in the past: _"To prevent reflows, specify the width and height of all images, either in the HTML **<img>** tag, or in CSS."_ [(Source)](https://developers.google.com/speed/docs/best-practices/rendering). 





And in responsive web design we are taught to not specify width and height of images, but to make them flexible with: **_img{max-width:100%;}_**. So in order to get the flexibility that responsive images offers we need to sacrifice some rendering speed. Right?





I am sure you have experienced reflow on mobile sites on a bad connection: you load a page, start to read the page, scroll down and then the content seemingly "jumps up and down" because of the reflow. This is because the browser does not know the dimensions of the image so it cannot reserve space for it. So when the image is loaded, it will have to insert it into the page, and move away everything that is below and right of it and do a reflow.






UPDATE: The following technique is based on an article I wrote about [responsive embeds](http://andmag.se/2011/11/responsive-embeds/) that again is based on an article by Thierry Koblentz called [Creating Intrinsic Ratios for Video](http://www.alistapart.com/articles/creating-intrinsic-ratios-for-video/).





I have put up a test page that simulates a slow connection so that we all can experience the pain together. To feel maximum pain, scroll down right after you load up the page. [Experience reflow.](http://andmag.se/responsive-images/reflow.html)





Still there? Great, hope there were minimal casualties.




## A solution




There is one prerequisite to this solution: you need to know the aspect ratio of the image. Let me explain the technique.





## No more img{max-width:100%}




Yes, that is correct. We are not using one of the most fundamental things in responsive web design. Instead we use the [responsive embeds](http://andmag.se/2011/11/responsive-embeds/) technique. This means that we set a wrapper div around the image and use the "padding-bottom" trick to make a div that keeps a certain aspect ratio:




The markup
[code]
<div class="embed-container ratio-16-9">
      <img src="imgage.jpg"/>
</div>
[/code]






The CSS, we add a few aspect ratios that we can use in our code:
[code]
.embed-container {
    position: relative;    
    height: 0;
    overflow: hidden;
    background-color:black;   
}

.ratio-16-9{
    padding-bottom:56.25%; /* 9/16*100 */
}

.ratio-4-3{
    padding-bottom:75%; /* 3/4*100 */
}

.ratio-1-1{
	padding-bottom:100%; /* ... */	
}
[/code]






Then, it's just a matter of setting the image to position:absolute and top left aligned:

[code]
.embed-container img{
    position: absolute;
    top: 0;
    left: 0;
    width:100%;
}
[/code]





Voila.





Sidenote: You can also use preprocessors like LESS to calculate the padding for you:

[code]
@ratio-16-9: (9%/16%*100%);
@ratio-4-3: (3%/4%*100%);
@ratio-1-1: (100%);

.ratio-16-9{padding-bottom: @ratio-16-9;}
.ratio-4-3{padding-bottom: @ratio-4-3;}
.ratio-1-1{padding-bottom: @ratio-1-1;}
[/code]






## How about max-width?




Since height of the div is calculated based on width on the parent div, we need to set max-width on the parent div if we want to limit the size of the image. This can be a drawback, but since the whole technique is based on that you know something about your images, it should be possible.






## The result - demo




And if we use the same technique as before to simulate a slow connection you can see that we now have a reserved space for the image (I use black background for clarity. And again, scroll down to experience the lack of reflow): [The demo without reflow!](http://andmag.se/responsive-images/no-reflow.html)






In this technique we reserve space for responsive content without specifying widht or height in pixels and we are not using JavaScript to calculate dimensions. Comments? Does anyone have alternative solutions?





UPDATE: A follow up article on how to also lazy load and multiserve images using this technique is [here](http://andmag.se/2012/10/responsive-images-lazy-load-and-multiserve-images/). 
