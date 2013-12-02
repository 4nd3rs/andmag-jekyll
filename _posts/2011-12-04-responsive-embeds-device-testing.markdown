---
author: admin
comments: true
date: 2011-12-04 22:51:29+00:00
layout: post
slug: responsive-embeds-device-testing
title: Responsive embeds - device testing
wordpress_id: 146
categories:
- Device detection
- Responsive Web Design
- RESS
- Slideshare
- Vimeo
- YouTube
---

I recently wrote about [responsive embeds](http://amobil.se/2011/11/responsive-embeds/) and how you can scale video and iframes to fit on a responsive website. I have now done tests on some mobile devices, and the results are pretty good for the responsive embed technique; but not so good for the content inside of the embed...


<!-- more -->


## Test setup


 



  * Nokia Lumia 800 with Windows Phone 7.5


  * Sony Ericsson Xperia X10 Mini Pro (SKE17i) Android 2.3.3


  * Sony Ericsson Xperia X10 Mini Pro (U20i) Android 2.1-update 1


  * Nokia C7 with Symbian Anna


  * Samsung GT-S8500 with Bada 1


  * iPhone 4S with iOS 5.0.1





## "Aw fiddlesticks!"




I tested Vimeo, Youtube and Slideshare embeds on all devices and wanted to know: a) Does the responsive embed technique work for mobile devices? b) Does the content inside of the embed work? Let's look at each device and how it looks.





### Nokia Lumia 800


![](http://amobil.se/wp-content/uploads/2011/12/IMG_0062.jpg)WP7.5 not getting any video love


Windows Phone 7.5 is the only non-webkit device in the test. The site renders fine and the responsive embed technique is also working as expected, but videos are not showing up. This is a bit surprising as I was under the assumption that the WP7.5 had [HTML5 video support](http://windowsteamblog.com/windows_phone/b/wpdev/archive/2011/10/13/html5-video-support-in-ie9-mobile.aspx).




UPDATE: Some videos are working on YouTube, but not my original test video. I changed it and the device plays the video.





### Sony Ericsson X10 Mini Pro (SK17i)


![](http://amobil.se/wp-content/uploads/2011/12/IMG_0044.jpg)Press play on tape


No problem at all with this device, all working as it should, but after all, this is a device with a new Android build and also one of the first devices with [WebGL support](http://developer.sonyericsson.com/wp/2011/11/29/xperia-phones-first-to-support-webgl/).





### Sony Ericsson X10 Mini Pro (U20i)


![](http://amobil.se/wp-content/uploads/2011/12/IMG_0056.jpg)Nope


This is the previous version of the X10 Mini Pro. It has a 240px screen and an older android version. Vimeo and Slideshare is working, but not YouTube.





### Samsung GT-S8500


![](http://amobil.se/wp-content/uploads/2011/12/IMG_0066.jpg)Vimeo wins the "best video playback error message of the year"


Not sure how Bada 2 performs, but Bada 1 users will get no videos from embed code. Slideshare is ok tough.





### Nokia C7


![](http://amobil.se/wp-content/uploads/2011/12/IMG_0052.jpg)Symbian Anna


This is a Symbian Anna device running Webkit, but no touch or swipe support so Slideshare is giving it the "navigate with arrows"-version. Vimeo and YouTube is not working.





### iPhone 4S




Not sure why I botherd to included it in the test... Yes it all works.





## All results





   

DeviceVimeoYou TubeSlide shareEmbed technique
   

Nokia Lumia 800
        
X
      
✓
      
✓
✓

   

SE X10 Mini Pro (SKE17i)
✓
✓
✓
✓

   

SE X10 Mini Pro (U20i)
 
✓
      
X
      
✓
✓

   

Samsung GT-S8500
       
X
      
X
      
✓
✓

   

Nokia C7
               
X
      
X
      
✓
✓

   

iPhone 4S
✓
✓
✓
✓





## Conclusion




The responsive embed technique is working fine on all tested devices and browsers, but after all, it is a very simple piece of code with just some plain HTML and CSS. The problem is that we do not have control of the stuff that is inside of the iframe. Slideshare works for all device, so this is a video problem. I know from experience that **video + mobile devices = asking for trouble** and did not expect this to work on the older devices. I am however surprised that Windows Phone 7.5 is not getting videos. When I go directly to YouTube or Vimeo it is in fact serving me videos on that device, so it looks like it is a problem with the way they handle the embed.





One solution to this problem is to just serve a YouTube/Vimeo link to the devices that does not support the embed and let the users open the video on the YouTube/Vimeo sites. The problem (except from the fact that you are linking the users out from your site) is that this is not testable in feature detection. So we would need to store the knowledge somewhere and do a conditional test on the serverside. I will do some more testing on this and post a possible solution for it once I have a demo up and running.






UPDATE: I have created a fallback solution for devices that does not support the embed by using server side techniques: [Responsive embeds + RESS](http://amobil.se/2012/01/responsive-embeds-ress/)
