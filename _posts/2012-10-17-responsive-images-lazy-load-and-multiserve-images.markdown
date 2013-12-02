---
author: admin
comments: true
date: 2012-10-17 17:24:22+00:00
layout: post
slug: responsive-images-lazy-load-and-multiserve-images
title: Responsive images - how to lazy load and multiserve images
wordpress_id: 401
categories:
- Responsive Images
- Responsive Web Design
tags:
- lazy load
- multiserve images
- responsive images
- responsive web design
---


I recently wrote about how we can prevent browser reflow when serving up flexible images by reserving space for the image so that the page will not reflow when the image is downloaded by the browser. This is done by using a [padding-bottom trick](http://andmag.se/2011/11/responsive-embeds/) that enables us to specify the height as factor of the width. This is a technique that works especially good for slow connections and slow CPU's.







And this technique makes it much less expensive to insert images with JavaScript. Loading images with JavaScript has been a big no-no because of the reflow and delay it causes. But now that we have eliminated reflow, we can look at loading images this way again. And keep in mind, what we care about is the perceived speed for the user, not how many milliseconds (or seconds...) it actually takes to load it up. And since we now use JavaScript, another door openes up to us: we can choose which image to load based on the screen size and pixel density of the device.







So if we expand on the markup of the previous post, we have now added some image version information to data attributes on the noscript tag. The img inside the noscript tag is used if JavaScript is not enabled.

[code]
<div class="lazy-load embed-container ratio-16-9">
    <noscript data-alt="img" data-src-240="img/climb3_240.jpg" 
        data-src-320="img/climb3_320.jpg" 
        data-src-480="img/climb3_480.jpg"
        data-src-640="img/climb3_640.jpg"> 
            <img alt="img" src="img/climb3_480.jpg"/>
    </noscript>
</div>
[/code]







And working from this it is quite easy to use a script to load the correct image based on screen width of the device. We can also multiply the width with devicePixelRatio so that we get better quality on screens with high pixel density.

[code]
//my code, so I get to choose the namespace name :-)
ANDMAG = {};

//get pixel ratio, default to 1
ANDMAG.devicePixelRatio = window.devicePixelRatio || 1;

//screenwidth  = width * pixelratio
ANDMAG.screenWidth = window.innerWidth * ANDMAG.devicePixelRatio;

//get images blocks and loop through them
ANDMAG.lazyLoadImages = function(){
    var lazyloadUs = document.getElementsByClassName("lazy-load");                
    for(var i = 0; i &amp;lt; lazyloadUs.length; i++){       
        ANDMAG.lazyloadImage(lazyloadUs[i]);
    }
}

//insert 'correct' image
ANDMAG.lazyloadImage = function(lazyLoadMe){
    
    var noscriptTag = lazyLoadMe.children[0];

    var imgAlt = noscriptTag.getAttribute("data-alt");
    var imgSRC240 = noscriptTag.getAttribute("data-src-240");
    var imgSRC320 = noscriptTag.getAttribute("data-src-320");
    var imgSRC480 = noscriptTag.getAttribute("data-src-480");
    var imgSRC640 = noscriptTag.getAttribute("data-src-640");

    //create element with correct size and insert it
    var img = document.createElement("img");

    if (imgAlt) {
        img.setAttribute("alt", imgAlt);
    }

    if(ANDMAG.screenWidth &amp;lt; 320){
        img.setAttribute("src", imgSRC240 );
    }else if(ANDMAG.screenWidth &amp;lt; 480){
        img.setAttribute("src", imgSRC320 );
    }else if(ANDMAG.screenWidth &amp;lt; 640){
        img.setAttribute("src", imgSRC480 );
    }else{
        img.setAttribute("src", imgSRC640 );
    }
    lazyLoadMe.appendChild(img);
}

// run the code
ANDMAG.lazyLoadImages();
[/code]





## The result









  * * No reflow


  * * Images only load once


  * * No .htaccess, PHP or backend hack


  * * Small size to small screens


  * * Not dependant on cookies


  * * Cachable


  * * Sensible fallback if JavaScript is turned off



Example on how page size varies: (Taken from the [demo site](http://andmag.se/responsive-images/)):







  * * When getting 240px images: **500kb**


  * * When getting 320px images: **644kb**


  * * When getting 480px images: **902kb**


  * * When getting 640px images: **1.13mb**





## Demo and code





See the solution in action: [http://andmag.se/responsive-images/](http://andmag.se/responsive-images/)  

The code is available on github: [https://github.com/4nd3rs/responsive-images](https://github.com/4nd3rs/responsive-images)

I would really appreciate (both positive and critical) comments or improvement suggestions to this solution!






## UPDATE




Added alt attribute to the image tag for validation and accessibility.
