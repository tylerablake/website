---
layout: post
title: "Accessing Native APIs with NativeScript"
excerpt_separator: "<!--more-->"
categories:
  - NativeScript
tags:
  - Intro
  - Overview 
  - NativeScript 
last_modified_at: 2018-08-03T13:30:00-00:00
---

One of the biggest advantages of NativeScript is the ability to access native device API's. In this post I'll show you how.
<!--more-->

Many other hybrid frameworks don't allow you to access device API's which causes limitations to app capability and performance. At first it sounds intimidating especially if you haven't written any Swift/Java code before but it will be a lot less scary after this post.



1. First let's navigate to the app root directory and run this command to add TNS Platform Delcarations

    `npm install tns-platform-declarations --save-dev`

2. Now, let's run the following command to create an empty reference.d.ts file

    `touch reference.d.ts`

3. Open the reference.d.ts file inside of your preferred IDE and add the following lines.

    `/// <reference path="./node_modules/tns-platform-declarations/ios/ios.d.ts" />`        
    `/// <reference path="./node_modules/tns-platform-declarations/android/android.d.ts" />`

**Note: If only developing for iOS or Android and not both, comment out the reference path for the platform you are not developing for, this helps speed up your development experience greatly!**


4. Save the file and now you are ready to start accessing native device API's!


In steps 1-4 we basically added intellisense for native API's, without doing that it is very painful to develop using native API's if you don't know the API's by memory.


Let's look at how to use this new knowledge to do some cool stuff!

First let's add an element to the page, in this case a button.

![ViewChild Button]({{site.url}}/assets/images/viewChildButton.png){:class="img-responsive"}

Then let's retrieve access to that element (in this case it is a button) inside of our component using the `@ViewChild` directive.

![ViewChild Reference]({{site.url}}/assets/images/viewChildReference.png){:class="img-responsive"}

That gives us a reference to the element, but since we are using NativeScript that element reference isn't quite the "Native" access we are looking for, in order to do that we need to drill into the exampleButton.


Here is an example of how to do that in iOS:

![Native iOS Element Reference]({{site.url}}/assets/images/nativeIosButtonReference.png){:class="img-responsive"}


Perfect! We have a button, and a reference to the Native element, in this case since we are building for iOS we have a reference to a `UIButton`.

Unfortunately, I have no idea about all of the possibilities that come with a UIButton....but this is where steps 1-4 from earlier come in. What happens if we type `iosButton.`?


![Native iOS API Intellisense]({{site.url}}/assets/images/nativeApiIntellisense.png){:class="img-responsive"}


**So many APIs!!!!!!**

<img src="{{site.url}}/assets/images/soManyApis.png" class="img-responsive" height="250" width="250">


Luckily since we added TNS Platform Declarations earlier, we now have access to "Go To Definition" on these native classes.

![Go To Definition]({{site.url}}/assets/images/goToDefinition.png){:class="img-responsive"}

Now you can drill into the `userInteractionEnabled` property and see all 15,000+ lines of properties and methods we have access to within `UIKit`, and that is just 1 of the many files for native iOS API's!

![API Reference File]({{site.url}}/assets/images/apiReferenceFile.png){:class="img-responsive"}



Now you can do all sorts of extra customizations to your apps. These steps can be replicated on all UI controls, including ListViews, Layouts, etc.


If you have any questions or comments feel free to leave them below. If you would like more info on this topic check out some of the following resources:


A presentation by Robert Laverty: [Robert Laverty Presentation](http://www.youtube.com/watch?v=zCdbrkmvdVI "Robert Laverty Presentation Link")

And as always, stop by and check out the [NativeScript Docs](http://docs.nativescript.org "NativeScript Docs Link") :)

