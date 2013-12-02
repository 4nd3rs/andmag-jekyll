---
author: admin
comments: true
date: 2012-11-30 23:18:58+00:00
layout: post
slug: its-evolution-baby
title: It's evolution, baby!
wordpress_id: 450
categories:
- Feature detection
tags:
- feature detection
- supports
---


"It's evolution baby". The voice of Eddie Vedder singing [Do the evolution](http://open.spotify.com/track/12d8CMvcWNBrJ7rMdT1kmt) popped up in my head when I first read about the proposed [@supports](https://developer.mozilla.org/en-US/docs/CSS/@supports) at-rule.







![](http://andmag.se/wp-content/uploads/2012/12/evolution.jpeg)






As a mobile old timer this makes me a very happy web developer. To me, this is the best thing that happened to the web since mediaqueries. Just look at all the web frameworks out there that the web "cannot live without" like jQuery, Modernizr, HTML5shiv etc. There are also server side frameworks that do browser detection that are used on cache servers, CDN's, video transcoders etc. These frameworks exist because of the diversity of the web and because the web has been so fragile that we have had little chance of making it work across devices without these tools. 







The method of the frameworks, shivs, polyfills and solutions are fundamentally the same:

    
    
       if support for feature X -> do A
       else -> do B
    





	 The difference lies in how they detect the support. And that is about to go away now. In the future you can just ask the browser: hey, how about display:flexbox? no? ok, here, have display:table instead. 






	 And this is huge mainly because it will **save us a lot of development time** and it will help to move the web forward. Will [VanillaJS](http://vanilla-js.com/) kill jQuery and @supports kill Modernizr? I hope I live to see it happen. Guys and gals:







    
    
       @supports (display:future){
          .music-in-my-head{
             content('It's evolution baby');
          }
       }
    






_

Image credit: http://lockerz.com/u/markickass/decalz/20021999/evolution_baby_

_
