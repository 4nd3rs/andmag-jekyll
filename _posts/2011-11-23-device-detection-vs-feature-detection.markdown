---
author: admin
comments: true
date: 2011-11-23 22:25:19+00:00
layout: post
slug: device-detection-vs-feature-detection
title: Device detection vs. Feature detection
wordpress_id: 89
categories:
- Device detection
- Feature detection
- RESS
---

Comparing Server side device detection and Feature detection is like comparing a hammer to a screwdriver. You can probably get a nail in a wall with a screwdriver and you can probably get a screw in a wall with a hammer. In this post I will try and explain by example how you should use device detection together with feature detection and that they are not to sides of the same coin.
<!-- more -->


## Been there, done that?


So first, let's look at classic scenario I think most web developers have faced when talking to clients:
- Hey developer, can we use this cool new feature I just read about?
- Yeah, but it will only work in the latest WebKit browsers.
- Webkit?
- It will work on most Macs, iPhones, iPads and some Androids, but probably not too good on a PC or a BlackBerry.
- Works on my iPhone! Do it.
- Eh... Ok. So what about those other devices?
- Give them a fallback version. You can do that right?
- Yes sir.

So what does the developer do? He needs a way to find out if this feature works in the browser. So let's say that the feature in question is an image gallery that should have touch+swipe and animation support, like the one on Boston Globe. Devices without touch will get navigation links. Devices without animation will just swap images without animation.

[![](http://amobil.se/wp-content/uploads/2011/11/The-Boston-Globe-300x106.png)](http://amobil.se/wp-content/uploads/2011/11/The-Boston-Globe.png)

So first thing he does is to check out feature detection with [Modernizr](http://www.modernizr.com/). And good news, he can check for touch and animation support. So he goes and create a JavaScript implementation that does the logic of giving the right version to the right device and also serve a fallback version if those features are not available.

So the implementation is ready and he starts testing. Works fine on standard web browsers, and if they do not have animation support they just get the fallback. Then he test mobile. Turns out, most mobile devices has animation and touch support, but many of them does a crappy job at doing the animation. Android 3.0 is especially bad. So Feature detection says that it works, and it does, but it's not really usable. Congrats, you have found a feature detection "false positive".


## Bad, worse, worst?


![](http://www.gotyabythetail.com/3monkeys_sm.jpg)

What happens next? He have (at least) three choices:



	
  1. Stick fingers in ears and sing "lalalalalalala". (Ignore it and hope his client only test on iPhone)

	
  2. He can start to write stuff like "if (UserAgent contains("Android 3")) -> doFallback". He only does this if he gets a positive result from the feature detection. ("UserAgent sniffing").

	
  3. Use server side device detection. Add a capability "crappy_css_animation" and set it to true for the devices that it did not work on. Use the new capability in the code.


You can argue which one of these options is worst, but I think most developers consider doing option 1) or 2). And many does not quite understand the difference between 2) and 3). So lets look at these two options.


## User Agent sniffing


![](http://www.onlyfunpics.com/funnypics/stinky_job.jpg)

If someone created a list of hated technologies and techniques on the web, this will probably be up there together with Flash and IE6.

Testing for UserAgent in code (option 2) is a bad thing for many reasons:



	
  * Not very reusable, you are probably duplicationg code and putting these if tests all over the place

	
  * You are probably doing it wrong. What it this issue fixed in Android 3.1? You will then need to update your test.

	
  * What happens when you discover that HTC Android, Huawei Android and ZTE Android have the same issues? (They do). But it works smooth on Samsung Android and Sony Ericsson Android. It's hard to maintain. And there are a lot of devices that you need to add to your list.




## Device detection


[![](http://amobil.se/wp-content/uploads/2011/11/Encyclopedia-1-300x199.jpg)](http://amobil.se/wp-content/uploads/2011/11/Encyclopedia-1.jpg)

This thing is often misunderstood by people that has not worked with it. You should look at it as a "knowledge base" and as a framework more than just a list of User Agents. It is as [future friendly](http://futurefriend.ly/) as an encyclopedia, but what is the alternatives?

Here is how you can work with it:



	
  * You insert a new capability into the framework. "crappy_css_animation". You default it to false, but set it to true for the device where you have found an error. Note that this test will only run if feature detection says "true".

	
  * Your code now only contains "if (crappy_css_animation) -> doFallback", so you have moved the ugly part to a place where it is more maintainable.

	
  * You will still have to maintain the device bug list, but the framework makes detection more reliable and provides you with a nice fallback system so you will probably have to add it at 3-4 places.

	
  * The problem of new devices hitting the market where the issue is fixed, remains. This is the biggest problem with device detection right now, if you start using it, you need to continue maintain it. There are companies that can do it for you, but those companies does not work for free. But you might end up saving money in the end.


Today there are basically just two options if you would like to do server side device detection. WURFL that is currently managed by [Scientia Mobile](http://scientiamobile.com) or you can use [DeviceAtlas](http://deviceatlas.com/). Both systems offer cloud services so that you do not need a lot of code to use it. They provide a lot of interesting capabilities out of the box, but for me, the framework where you can add your own capabilities is just as interesting. 


## Best of both worlds?


In my opinion, the developer in the example above should use the best of both worlds. Use feature detection to find if a device supports a feature, and then use device detection to remove false positives. Sure, the solution needs some maintenance, but I want to build solutions that works great on all devices today, not half good solutions that does not work for all devices. So for me the choice is easy, I choose to use the best of both worlds.
