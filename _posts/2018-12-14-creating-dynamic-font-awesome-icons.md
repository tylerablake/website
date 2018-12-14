---
layout: post
title: "Creating Dynamic Font Awesome Icons"
excerpt_separator: "<!--more-->"
categories:
  - NativeScript
tags:
  - Intro
  - Overview 
  - NativeScript 
last_modified_at: 2018-12-14T13:30:00-00:00
---

Font Awesome icons are great, but sometimes we want to change them, their color, or size dynamically. Let's see how to do that with NativeScript
<!--more-->

For this example let's say we have a list that we want to show battery life of items.

Here is what we want the finished product to look like:


![Battery Indicator Screenshot]({{site.url}}/assets/images/batteryIndicatorAppScreenShot.png){:class="img-responsive"}


### Pick your icons
Here are the unicode for each of the icons we want to use

* 0% - 0xf244
* 25% - 0xf243
* 50% - 0xf242
* 75% - 0xf241
* 100% - 0xf240


### Build out your UI

![Battery Indicator View Code Screenshot]({{site.url}}/assets/images/batteryIndicatorViewScreenShot.png){:class="img-responsive"}


* Notice the **getBatteryColor()** and **getBatteryCode()** methods which are bound using 1 way binding with `[]` to our component.


### Hook up your component

* **DISCLAIMER**
Please don't hate on my `if` and `else if` lines, I thought that format would be easiest to follow :)

![Battery Indicator Component Code Screenshot]({{site.url}}/assets/images/batteryIndicatorComponentScreenShot.png){:class="img-responsive"}

* In the component we just need to determine which color hex or unicode to return for each item in the `ListView`

* This shows some **short circuit** evaluation, which means exit the code the moment a condition is met, instead of testing a bunch of conditions then exit.

Feel free to try and implement something similar into some of your own apps!

If you have any questions or comments feel free to leave them below and as always, stop by and check out the [NativeScript Docs](http://docs.nativescript.org "NativeScript Docs Link") :)
