---
author: admin
comments: true
date: 2013-01-07 23:04:44+00:00
layout: post
slug: creating-high-resolution-assets-with-grunticon
title: Creating high resolution assets with grunticon
wordpress_id: 464
categories:
- SVG
tags:
- devicePixelRatio
- grunt
- grunticon
- nodejs
- phantomjs
- svg
---

[Grunticon](https://github.com/filamentgroup/grunticon) by [Scott Jehl](https://twitter.com/scottjehl)/[Fillamentgroup](http://filamentgroup.com/) is a brilliant little tool that helps you generate the necessary assets in order to serve icons as SVG and at the same time handle fallback for older browsers. It takes a folder with SVG files and generates the following:






	
  * A CSS file with base64 encoded SVGs (note that you only get one CSS file and one HTTP request for all your icons!)

	
  * A CSS file with base64 encoded PNGs

	
  * PNG icons and a CSS file that point to the generated icon files

	
  * A JavaScript file that serves CSS files based on a feature detect





Grunticon is built as a [grunt](http://gruntjs.com/) task that and uses [PhantomJS](http://phantomjs.org/) to generate PNGs from the SVG files. It renders a page with an SVG and grabs a screenshot of it and saves that as an PNG. 





We are using grunticon on the project that I am currently working on, but needed a small enhancement to it. We needed it to generate 1.5x and 2x versions of the PNGs. The 1.5x version will be served to Android 2.x devices, and the 2x version will be used in an API in order to give apps accessing it high resolution graphics (those apps are probably not using SVG).





## grunticon-highrespng




So I modified grunticon to also be able to save the PNGs in different sizes by modifying to zoomfactor of the rendered SVG. The desired formates is specified in the settings, so if you like 1, 1.5x and 2x PNG graphics in your project you just specify:



[code]
pngpixelratio: [1, 1.5, 2]
[/code]




And the task will generate 1x, 1.5x and 2x fallback PNGs, base64 encoded datauri PNGs and the necessary CSS files in those formats. It also generates a loader JavaScript file that will feature detect by using devicePixelRatio together with SVG and datauri tests to decide which version to serve to the browser. This is how the output folder looks after a run:






![](http://andmag.se/wp-content/uploads/2013/01/Skärmbild-2013-01-07-2314.png)






## Install




See the "[getting started](https://github.com/4nd3rs/grunticon)" section on github if you do not have nodejs, phantomjs and grunt installed. Otherwise just install grunticon-highres by running:


[code]npm install grunt-grunticon-highrespng[/code]


### Resources






  * [grunticon-highrespng on Github](https://github.com/4nd3rs/grunticon)


  * [grunticon on Github](https://github.com/filamentgroup/grunticon)





Enjoy!





_Thanks to Filamentgroup for another brilliant tool, for making it open source and for letting me share this little modification!_
