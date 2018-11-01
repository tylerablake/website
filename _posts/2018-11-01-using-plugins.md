---
layout: post
title: "Using Plugins"
excerpt_separator: "<!--more-->"
categories:
  - NativeScript
tags:
  - Intro
  - Overview 
  - NativeScript 
last_modified_at: 2018-11-01T10:30:00-00:00
---

What are plugins? How can they help us? How do we use them? Let's see how to install and use plugins with NativeScript
<!--more-->

## What is a plugin?

A plugin is basically a package that someone has created that we can use in our NativeScript apps

Common plugins are basically wrapper code around native components like the [nativescript-camera](https://github.com/NativeScript/nativescript-camera "nativescript-camera link") plugin

Plugins are NOT required but they do help

## How do they help?

Most plugin creators have already written the code that you would use anyway. 

Typically they are just wrappers around native code 

For example in the `nativescript-camera` plugin, they have exposed a `camera.isAvailable()` method that we can use to check if a device camera is available

This means we can just install the plugin and use this method without having to manually check if the device has a camera and if it is working

## How do we use them?

Most NativeScript plugins have good documentation, at the very least they have installation notes

Typically you can install NativeScript plugins with this command

`tns plugin add pluginName`

For example

`tns plugin add nativescript-camera`

would install the `nativescript-camera` plugin in your app


## Which plugins should we use?

The best place to look for plugins is on the [NativeScript Marketplace](https://market.nativescript.org/ "nativescript marketplace link")

This is where you will find plugins for your NativeScript apps

Use **verified** plugins when you can as these have been reviewed by the NativeScript team and supported by the team

The criteria to be a **verified** plugin is the following:
* Must be transpiled correctly (tsc) and pass tslint checks
* Must have a demo app
* Should be eligable for Angular and non-Angular apps
* Must build successfully on the latest iOS version of NS
* Must build successfully on the latest Android version of NS
* Must be bundled with webpack and built successfully for the latest iOS version
* Must be bundled with webpack and built successfully for the latest Android version
* Weekly builds with Travis CI must pass
* README must clearly explain limitations and features
* There is a license file
* Reviewed by NS team

As we can see, verified plugins are definitely the most stable plugins, that is why we should use a verified plugin when we can

Non-verified plugins can be just as good though so check them out too but be careful

It is also a good idea to look at how many downloads the plugin has, if it has a lot of total downloads and a lot of weekly downloads, it is probably a good plugin

Verified plugins can be found with a verified icon next to their name

This is the `nativescript-imagepicker` plugin, I'll show you what questions I ask myself when I think about using a plugin


* **Is it verified?**
It has the verified icon, so it is
* **Is it popular/ does it have a lot of downloads?**
It has 3.3k/month, 689 last week, and 151 yesterday
* **Is it currently passing all builds?**
The build stats near the bottom tell us if it is passing, it is
* **Does it have the functionality I need?**
Yes
* **Does it have any limitations?**
I don't see any limitations listed for the plugin currently

![Verified Plugin Page]({{site.url}}/assets/images/verified-plugin-page.png){:class="img-responsive"}

If the plugin has the answers to those questions that I am looking for then I will try it

Not to worry, if you find a plugin doesn't work for you, you can easily uninstall it with the following command and start over with a new plugin

`tns remove plugin pluginName`

Now we know how to find a plugin, check if we should use it, install it, and remove it if we need to.

Swing by the [NativeScript Marketplace](https://market.nativescript.org/ "nativescript marketplace link") and start adding plugins to your NativeScript app!

If you have any questions or comments feel free to leave them below and as always, stop by and check out the [NativeScript Docs](http://docs.nativescript.org "NativeScript Docs Link") :)


