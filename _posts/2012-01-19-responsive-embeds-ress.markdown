---
author: admin
comments: true
date: 2012-01-19 23:38:41+00:00
layout: post
slug: responsive-embeds-ress
title: Responsive embeds + RESS
wordpress_id: 194
categories:
- Device detection
- Responsive Web Design
- RESS
- YouTube
---

After writing about [responsive embeds](http://amobil.se/2011/11/responsive-embeds/) and then [doing some device testing](http://amobil.se/2011/12/responsive-embeds-device-testing/) on how responsive embeds perform in real life, I deciced to take it one step further; to use server side technologies in order to make the video work for all devices. 


<!-- more -->



Using server side techniques on a responsive web design site is often called [RESS](http://www.lukew.com/ff/entry.asp?1392) (Responsive design + Server side components). And I am going to user server side logic to make the embed work on as many devices as possible. I am using YouTube videos in this example because I know the YouTube mobile site works well also for devices that does not support the embed. I am also using server side device detection with [WURFL](http://scientiamobile.com) in order to define the devices that I found not to work. For these devices I will create a simple link to YouTube instead of serving them the iframe. The default behavior will be to serve the iframe, so new/unknown devices will get the preferred experience.





I am using WURFL and a WURFL API, but I am not going to use any of the WURFL capabilities since there are no capabilities that meets my need. I found that many people have a problem with WURFL capabilities and say that it's missing many capabilities, but that is really not an argument against tools like this, since it's very easy to create your own capabilities. So I am just using WURFL as a framework to help me out with the detection and I will create my own capability:

[code]
<group id="third_party">
    <capability name="youtube_embed" value="false"/>
</group>
[/code]



I will define this capability to false for the device groups where the YouTube embed was not working. I am defining it on a OS level, and not for specific devices (that would be a real mess), so there are not many entries that are needed:







  * **Windows Phone 7**: false


  * **Android**: false


  * **Android 2.2**: true


  * **Nokia Symbian**: false


  * **Samsung Bada**: false





Note that I am disabling it for generic Androids, but enabling it again for Android 2.2. That means all old Android will get the fallback solution, but the new ones will get the iframe. This works well because of WURFL's hierarchical fallback system.





I created a simple WordPress plugin in order to use it on this blog. The plugin is grabbing the capabilities via a REST service and caching it. It then decides which version of the YouTube embed that it is going to serve to the user. It uses a screenshot from the video and a link to the YouTube site as a fallback. The nice thing about this is that devices that has a YouTube app will (most often) open the video in the native app. Here is the code that I end up with in my post:



[code]
[[youtube]TFWDUsvLCoE[/youtube]]
[/code]



Below is the plugin in action: 






[youtube text="See the Ultra-Trail du Mont-Blanc video"]TFWDUsvLCoE[/youtube]







I found this to work quite good, I have tested it on the some older devices and I get a link to YouTube and can watch the video on their mobile site. So now I have a backwards compatible video solution on my responsive web site by using some relatively simple server side techniques, and I can share videos with a lot more users than before.






Drawbacks? Well, I am basically maintaining how YouTube is working on mobile devices in my own database and I need to keep the info up to date. If YouTube starts supporting Windows Phone 7 in the embed I need to update that info in order to give those users an optimal experience (the site will still work with the fallback). That's a downside, but on the other hand I would rather that my website works on as many devices as possible today, than wait until they are supported. 






How about feature detection? If you know how to feature detect this, please let me know in the comments. (I do not think that it's possible :-) ). Also please let me know if the video is not working for you.



