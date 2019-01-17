---
layout: post
title: "Managing App Versioning on iOS"
excerpt_separator: "<!--more-->"
categories:
  - NativeScript
tags:
  - Intro
  - Overview 
  - NativeScript 
last_modified_at: 2019-01-17T17:30:00-00:00
---

Versioning your app's builds is great but managing that versioning can be a pain, in this post I'm going to show you how I manage versioning and hopefully help you out.
<!--more-->

### What is "versioning"?

"Versioning" in this context, means seeing a little `v 1.0` at the bottom of the page that your users land on when opening your app, which is typically the login page or home page.


### What's the problem?

When I first started developing NativeScript apps I manually updated the version on that landing page before each publish.

<!-- Sometimes I would forget to update it completely, or sometimes I would forget to update it in the middle of the build process. Then I would update it inside of XCode, which would increment the build number inside of HockeyApp, but not inside of my app. -->

Sometimes I would forget to update it, so a user might report a bug on build 35, but in reality they are on build 36, which makes finding and fixing that bug much harder.

Enough of that boring stuff, let's talk about how to "automate" it.

Something awesome I found is that you can actually pull data from your plist file, so you don't have to update your html file each time you update your plist file, here's how!

### Set the App Version

Given you set your version inside of your plist file like this:

![plist version number]({{site.url}}/assets/images/plistVersionNumber.png){:class="img-responsive"}

### Pull the App Version

Pulling the version is simple, first you need to add the NativeScript utils into your component. 

Add this line just below all of your imports for your component.

![import utils]({{site.url}}/assets/images/utilsScreenShot.png){:class="img-responsive"}

Then inside of your component you can use this to pull that version number.

In this case I'm setting a `version`, a component property, to the version number


![setting app version]({{site.url}}/assets/images/settingAppVersion.png){:class="img-responsive"}

Notice how you use the `key` to retreieve the value from your plist file

### Display the App Version

Now all you need to do is update your html to dispay that `version` property with data binding like so:


![setting app version ui code]({{site.url}}/assets/images/settingAppVersionUICode.png){:class="img-responsive"}


Which looks like this on a login page:


![setting app version ui]({{site.url}}/assets/images/settingAppVersionUI.png){:class="img-responsive"}

Feel free to try and implement something similar into some of your own apps!

If you have any questions or comments feel free to leave them below, or reach out to me. As always, stop by and check out the [NativeScript Docs](http://docs.nativescript.org "NativeScript Docs Link") :)
