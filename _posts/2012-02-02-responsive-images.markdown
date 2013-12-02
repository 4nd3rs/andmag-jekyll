---
author: admin
comments: true
date: 2012-02-02 00:11:38+00:00
layout: post
slug: responsive-images
title: Responsive images + server side components
wordpress_id: 255
categories:
- Device detection
- Feature detection
- Responsive Web Design
- RESS
---

People, I'm sorry. I know we do not need another post about responsive images, but I got inspired to try another responsive images approach after reading the article ["Responsive Images: How they Almost Worked and What We Need"](http://www.alistapart.com/articles/responsive-images-how-they-almost-worked-and-what-we-need/) by Mat Marquis on A List Apart. My approach is to use the proposed <picture> tag and implement it using server side components.


<!-- more -->


So Mat explains that one "solution" for the responsive images problem is to solve it in markup by using the <picture> tag in the same way as the <video> tag is implemented. Problem is, no browsers supports the <picture> tag (yet). 





## The solution




I went ahead and wrote some code that parses the <picture> and <source> tags and finds the correct image for the device. I am measuring device width on the client side in JavaScript and setting the value in a cookie. It is falling back to server side device detection if the cookie is not available, so that we get a "best guess" version of the image if we don't know the screen dimensions, instead of just serving the mobile one. I wrapped all this up in a WordPress plugin so that I can show it to you. Here is the html I am using for this site (simplified the src to make the example shorter)



[code]
<picture>
        <source src="1024.jpg" media="min-width: 800px" />
        <source src="640.jpg" media="min-width: 640px" />
        <source src="480.jpg" media="min-width: 480px" />
        <source src="320.jpg" />
        <!-- Fallback content: -->
        <img src="http://amobil.se/wp-content/uploads/2012/02/320.jpg" />
</picture>
[/code]



Try and resize the browser window and reload the site to see the effect. If you are on a mobile device, you need to switch orientation and reload. 




        
        
        
        
        
        ![](http://amobil.se/wp-content/uploads/2012/02/320.jpg)




So it's sort of a "serverside polyfill"... It's not doing anything fancy on the client side so the image will not change when you resize the window. On the other hand, it just results in one static <img> tag that is sent to the browser and optimized for the screen size that you have.





PS: If you want to see other responsive images hacks, and some that are similar to this one, there are plenty up at the Cloud Four blog: [Responsive Images](http://www.cloudfour.com/responsive-imgs/)
