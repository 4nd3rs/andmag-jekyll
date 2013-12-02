---
author: admin
comments: true
date: 2012-10-15 19:11:16+00:00
layout: post
slug: did-a-meta-tag-just-kill-the-mobile-splash-screen
title: Did a meta tag just kill the mobile splash screen?
wordpress_id: 386
categories:
- iOS6
- Mobile Internet
tags:
- iOS6
- mobile web
- splash screen
---

Well I certainly hope so!





Apple released a lot of new features to Mobile Safari in iOS6 and if you have not yet read about it, please do so in [this excellent post](http://www.mobilexweb.com/blog/iphone-5-ios-6-html5-developers). One of the new features is a meta tag called "apple-itunes-app". This will display a "smart app banner" on your site in a very gentle way:





![](http://andmag.se/wp-content/uploads/2012/10/Bild-2012-10-15-2029-2.png)


<!-- more -->


And adding the banner almost too easy, first you need to find the Apple iTunes ID from [iTunes Link Maker](http://itunes.apple.com/linkmaker/) and then add the link to your _**<head>**_ tag:

[code]
<meta 
  name="apple-itunes-app" 
  content="app-id=333903271">
[/code]





## Deep linking





By using an "app-argument" you can pass arguments to the app if the user has the app installed. The app needs to support the argument, but it means that the app can pick up the argument and let the user continue browsing the same content as he saw in Safari. This works well on Twitter where you can browse to a Twitter profile in Safari, click "open app" on the app banner and the Twitter app will open the same user you were browsing in Safari. Here is the meta tag that Twitter uses:
[code]
<meta 
  name="apple-itunes-app" 
  content="app-id=333903271, app-argument=twitter://user?screen_name=andmag, affiliate-data=partnerId=30&amp;siteID=UkOLawSuc90">
[/code]
You can also use the "affiliate-data-partnerId" if you participate in the [iTunes Affiliate Program](http://www.apple.com/itunes/affiliates/)






So owners of sites with "download my app splash screen" now have two options:






  * 1. Add the new app banner


  * 2. Be featured on [WTFMobileWeb](http://wtfmobileweb.com/)


