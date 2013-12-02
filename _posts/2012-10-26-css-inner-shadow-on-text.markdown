---
author: admin
comments: true
date: 2012-10-26 09:30:02+00:00
layout: post
slug: css-inner-shadow-on-text
title: How to set inner shadow on text in CSS (in webkit...)
wordpress_id: 431
categories:
- CSS
- Feature detection
---

Unlike the **box-shadow** property, **inner-shadow** does not support the **inset** attribute. The following code is NOT valid:
[code]
 text-shadow: inset 0px 0px 10px rgba(0,0,0,0.9);
[/code]







Which is a bummer, I really wanted to style the logo of my site in CSS and not use an image, font or SVG for it. But I came over a [clever hack](http://designshack.net/?p=35857) that solves the issue for us. 






## How it works




There are 5 steps that are needed to acheive this, and you can see the result of each of them below:




![](http://andmag.se/wp-content/uploads/2012/10/text-shadow.jpg)






[code]
.logo{
  font-size: 4em; /*step 1*/
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2); /*step 2*/
  color: transparent;/*step 3*/
  background-color: #F9F9F9;/*step 4*/
  background-clip: text;/*step 5*/
}
[/code]


How it works:




  1. 1. The normal style without any applied effects


  2. 2. The text when a black shadow with opacity applied


  3. 3. We hide the text the only thing visible is the shadow


  4. 4. We set the background color to the color we want the text in


  5. 5. We clip the background to the bounds of the text. This will make the shadow look like it is just on the inside of the text!








## Support




Background is a webkit specific property at this point.

UPDATE: Turns out it is tricky to feature test this unless you want to browsersniff. Modernizr has not yet found a good solution: [https://github.com/Modernizr/Modernizr/issues/199](https://github.com/Modernizr/Modernizr/issues/199)






Happy coding!
