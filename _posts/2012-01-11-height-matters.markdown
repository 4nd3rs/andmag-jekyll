---
author: admin
comments: true
date: 2012-01-11 23:29:40+00:00
layout: post
slug: height-matters
title: Height matters!
wordpress_id: 187
categories:
- Responsive Web Design
- Usability
---

Height is just as important as width when dealing with responsive web sites. I've seen so many responsive web design sites lately that are mobile **unfriendly** because they do not take the height of the device into account. Just consider the following example:




<!-- more -->






[![](http://amobil.se/wp-content/uploads/2012/01/iOS-Simulator-2-151x300.jpg)](http://amobil.se/wp-content/uploads/2012/01/iOS-Simulator-2.jpg)






The above example is from a Swedish site and as you see it's using massive amounts of screen real estate on the logotype. At the middle of the screen we see the first menu item, and only 2 of 4 menu items are visible... And is search really the first thing they want us to do? And worse, in the screenshot I have clicked the first menu item. The site reloads and what I see is that menu item marked as selected, and no indication that the content below the menu now in fact has changed. Clearly, not a "mobile first" site.







And this is just an example. Have a quick look through [mediaqueri.es](http://mediaqueri.es/) and you see that many of the sites are just delivering logo + navigation as the first view for mobile. The sites are adapted for the width of a mobile device, but not for the height. In fact, I wish [mediaqueri.es](http://mediaqueri.es/) would show the mobile screenshot in 320x480 instead of 320x800 like they do now. 







So a few simple words of advice:







  * Don't hav a logotype that takes up 50% of the screen

  * Make sure some of your content is visible on the first screen, otherwise users will have a hard time understanding that they have in fact navigated to a new page. 


  * Use a mobile device for your design and mockup work to visualize how little space you have to play with. Also, [display browser chrome on your mock ups](http://mobilewebbestpractices.com/visual-design/display-browser-chrome-on-mock-ups/).






You can also consider to use "height" in your mediaqueries to make sure you optimize the header of the site:

[code]
media screen and (max-height:460px) {
   .giantlogo{display:none}
}
[/code]



Also, have a look at Trent Waltons ideas about [vertical mediaqueries](http://trentwalton.com/2012/01/11/vertical-media-queries-wide-sites/) and how they can be used to change things like fonts based on the client height.





Height matters!





UPDATE: The site I used as an example has actually updated their site and made some improvements. The header of the site is much better now. The web is moving forward after all :-) Good work guys!





[![](http://amobil.se/wp-content/uploads/2012/01/radiotjanst_new-151x300.jpg)](http://amobil.se/wp-content/uploads/2012/01/radiotjanst_new.jpg)
