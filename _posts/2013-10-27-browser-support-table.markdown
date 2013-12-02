---
author: admin
comments: true
date: 2013-10-27 21:51:13+00:00
layout: post
slug: browser-support-table
title: Browser support table - for responsive websites
wordpress_id: 488
categories:
- Responsive Web Design
---

## Background


The following document is a modification of a [browser support standards](http://www.bbc.co.uk/guidelines/futuremedia/technical/browser_support.shtml) document created by BBC. The document was outdated and did not cover mobile browsers so I did some modifications and simplifications. The document is meant as a guide for Responsive Web Design projects and will give developers and clients a hint of what browser support they can expect and will give the development team guidance on how they need to focus their testing. It is not meant as a contract between the development team and the client. It is important that the development team use web standards, and browsers that are not mentioned on this list (such as TV browsers, game consoles, fridge browsers and smart watches) will probably work well, but they will not be actively tested by the development team.


## 1. Introduction




### 1.1. Scope of this Document


1.1.1. This standard applies to web browsers that are being used on desktop versions of Windows, Mac OS and Linux/Unix and mobil browsers that are being used on iOS, Android and Windows Phone.


### 1.2. Web Browser Support


1.2.1. The project members accept that the nature of the web medium is such that web pages cannot be produced in such a way as to be uniformly rendered in all browsers, so as to provide a consistent experience for all users. We accept that small variations in this experience are acceptable within the 'Levels of Support'.

1.2.2. Web browsers are assigned a 'Level of Support' by the project members. These levels of support are summarised in the Browser Support Table.

1.2.3. There's nothing wrong with using all the latest bells and whistles to support funky features of newer browsers, but we try to do it in a way that still allows users not supporting (or intentionally disabling) these features to access your basic content.


## 2. 'Levels of Support' definitions




### 2.1. Support Level 1 - supported web browser - Support definition


2.1.1. All content **MUST** be readable and usable and all functionality **MUST** work.

2.1.2. Variations to presentation of content **MUST** be minimised.

2.1.3. Where CSS layout is used, the CSS **MUST** be rendered by supported web browsers, so that a fully-styled version of the page is presented to the user.

2.1.4. Pages **SHOULD** be developed to maximise the user experience for users of the web browser with the highest proportion of users.


### 2.2. Support Level 2 - partially-supported web browser - Support definition:


2.2.1. All core content **MUST** be readable and usable and navigation **MUST** work.

2.2.2. Any degradation to (client-side) application functionality **MUST** be graceful degradation.

2.2.3. Any degradation to presentation **MUST NOT** obscure content.

2.2.4. Where CSS layout is used, you **MAY** choose to provide an unstyled version of the page to partially-supported browser.


### 2.3. Support Level 3 - unsupported web browser - Support definition:


2.3.1. No support or testing necessary.

2.3.2. Any web browsers not specifically listed in the support table **MAY** also be regarded as level 3; that is, unsupported.


## 3. Support table


3.1. The table below defines the levels of support that **MUST** be adhered to.







Browser
Version
Platform
Level





IE


8, 9, 10


Windows


1






IE


7


Windows


2






IE


WP 8


WP 8


1






IE


WP 7.5


WP 7.5


2






Firefox


latest


All


1






Chrome


latest


Windows & Mac


1






Opera


latest


All


2






Safari


5, 6


Mac


1






Safari


iOS 6, iOS 7


iOS


1






Safari


iOS 5


iOS


2






AndroidBrowser


Android 4.1+


Android


1






AndroidBrowser


Android 2.3Android 4.0


Android


2






Chrome


latest


iOS & Android


1






###  Notes:


**Browser Versions**




Pre v1.0, Alpha, Beta and Release Candidate builds are not supported.


#### Browser Abbreviations


FF = Mozilla Firefox, IE = Microsoft Internet Explorer, WP = Windows Phone


