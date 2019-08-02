---
layout: post
title: "Automated UI Testing in NativeScript"
excerpt_separator: "<!--more-->"
categories:
  - NativeScript
tags:
  - Guide 
  - NativeScript 
last_modified_at: 2019-08-01T20:42:00-00:00
---

Do you want a guide on how to set up automated ui testing for your NativeScript apps? Welp, here it is!
<!--more-->

This post outlines my experiences of working with the `nativescript-dev-appium` plugin and writing my tests manually. 

I have received a few messages requesting help with e2e testing so I wanted to get this post out there quicky. I will update it as I have more information to share, as well as write a few more blog posts on things like *Using the Appium Client* and *Using the appium-doctor to Diagnose Installation Problems*.

**Note:** This post contains my finds and gotchas along the way, I started by following the NativeScript docs on e2e testing [NativeScript E2E Guide](https://docs.nativescript.org/angular/tooling/testing/end-to-end-testing/overview "nativescript e2e testing guide"){:target="_blank"}

I did my setup on a Mac, so if you are on Windows or Linux, your installation process might be different. Please refer to the NativeScript guide above if you have issues or reach out in the [NS community Slack](https://www.nativescript.org/slack-invitation-form "nativescript community Slack invite link"){:target="_blank"} and I'll try to help you!

## Machine Setup

### Install Appium

1. Run `npm install -g appium`

You might have to run `sudo npm install -g appium`


### iOS Dependencies

1. Run `brew install carthage`
2. Run `brew install libimobiledevice --HEAD`
3. Run `brew install ideviceinstaller`
4. Run `brew install ios-webkit-debug-proxy`
5. Run `npm install -g ios-deploy`


### Android Dependencies

1. Run `brew install telnet`


## Project Setup

1. Run `npm install -D nativescript-dev-appium`

During the installation process you will be asked a few questions

1. What framework you are using (JS/TS, Angular, Vue) - I chose Angular
2. What is your preferred testing framework (Mocha, Jasmine, etc.) - I chose Mocha

**Note:** After installing I recommend you go to your `tsconfig.json` and add your new `e2e` folder to your `excludes` array

This brings us to our first **gotcha**!

#### Gotcha #1 - Running the Default Tests
The default tests generated when you install the `nativescript-dev-appium` plugin are for the hello-world-ts template.

If you used a different template the generated tests will likely fail


## Testing Workflow

1. Make changes to your app
2. Build your app `tns build ios|android`
3. Write your test
4. Run your test `npm run e2e -- --runType <capabilityName>`

`<capabilityName>` is the corresponding key to the simulator/device you want to run the tests against inside of your new `appium.capabilities.json` file

Example: `npm run e2e -- --runType sim.iPhone7`

**Note:** The first `--` is not a typo, I believe it is a flag to set `fullReset: true` and `noReset: false` in the appium.capabilities on the fly


If you ran `npm run e2e -- --runType sim.iPhone7` like me without having an iPhone7 simulator running, it should fallback to the simulator you have running, or atleast it did for me :)

If that command runs without any errors after a little bit a web browser tab should open, and the terminal should alert you of the results (in this case 0 passed 2 failed with information on why, see gotcha #1)

#### Gotcha #2 - App Permission Requests

My app has a location permission that immediately pops up, the tests will hang/fail but I manually accepted the permission alert from iOS and then the tests ran successfully

You can set up auto accept alerts by adding this line in the JSON body for the capabilityName you are using when running your tests, found in your `appium.capabilities.json` file

 `"autoAcceptAlerts": true`

 You have many other options you can use like 

`"locationServicesAuthorized": true`
`“autoDismissAlerts” : false`

For a full list of the different capabilities of both iOS and Android check the [Appium Docs on Capabilities](https://appium.io/docs/en/writing-running-appium/caps "appium capability docs"){:target="_blank"}


#### Gotcha #3 - Find Element By Image

With Appium you have many ways to find elements, one of them is `findElementByImage(base64String, threshold)` where you pass in a base64 string of your image and Appium will search for that image in the page using the supplied threshold.


Intellisense was telling me that method takes the `path` not the `base64` encoded string. 

I added the image to the `e2e/resources/images/projectName/iPhone 6` folder.

Then I updated the test to try `await driver.findElementByImage("blue_truck_icon@3x”)`

But then got the following error in the mocha reporter:

```
Error response status: 13, , UnknownError - An unknown server-side error occurred while processing the command. 

Selenium error: An unknown server-side error occurred while processing the command. 

Original error: opencv4nodejs module is required to use OpenCV features. 

Please install it first (npm i -g opencv4nodejs) and restart Appium. 

Read https://github.com/justadudewhohacks/opencv4nodejs#how-to-install for more details on this topic.
```

I tried to run `npm I -g opencv4nodejs` and got this error:

```
Error: failed to execute cmake --version, cmake is required to build opencv,

error is: Error: Command failed: cmake --version

/bin/sh: cmake: command not found
```

To get around this error I ran these commands

1. `brew install cmake` - to install cmake
2. `cmake —version` - to verify cmake installation

Then I tried to run `npm I -g opencv4nodejs` again, after installing what felt like 5 million files/dependencies/etc the installation succeeded

**Note:** You might want to make sure your laptop is plugged in, I lost about 20% battery during this step 😂

All that leads me to our next **gotcha**


#### Gotcha #4 - What does findElementByImage() expect? Path or base64??

**Note:** The `findElementByImage()` method is an experimental feature so you might want to avoid trying to use it if you can, but if you must, here is my experience. I hope it helps you! 🤞

I looked at the source code for `findElementByImage()` method and found that it is expecting the image fileName **without the extension**

Then it builds out a path to that file, and converts it to a base64encoded string before passing it to the Appium driver

So I tried using `driver.findElementByImage(imageName);` again but it didn’t work. 

I got the error `Error: The provided image does not exist!!!`

When the `findElementByImage()` method tries to create the `filePath` for the fileName you passed it, it looks in the following directory `e2e/resources/images/projectName/deviceName/fileName.png`

After verifying that the `generatedPath` by the `findElementsByImage()` method was correct I got the following error even though the image **was** on the screen at the time:

`Error response status: 7, NoSuchElement - An element could not be located on the page using the given search parameters`

I switched to search for an image in the ActionBar to test and see if I could get Appium findElementByImage() method to succeed but it didn’t.

#### Gotcha #5 - findElementByImage() - ImageThresholdMatch

The image I was search for was a pin using the Google Maps SDK, so maybe that's why the Appium driver couldn't find it

I switched to search for an image in the ActionBar to test and see if I could get Appium's `findElementByImage()` method to succeed but it didn’t...

The 2nd parameter for `findElementByImage()` is a `imageThresholdMatch`, which is a setting for how close the images must match to be returned by the driver

The `imageThresholdMatch` parameter is optional, and defaults to 0.4 if not passed

The range for the `imageThresholdMatch` parameter is 0 (no comparison) - 1 (pixel by pixel comparison)

When I passed in `findElementByImage(fileName, 0);` the test succeeded finally!!

After doing some more research I found some information regarding this `imageThresholdMatch` on the [Appium Docs on Finding Elements by Image](http://appium.io/docs/en/advanced-concepts/image-elements "appium find element by image docs"){:target="_blank"}

Under the **Related Settings** section, I read more into the `imageThresholdMatch`, here is what it said:

The OpenCV match threshold below which to consider the find a failure. 

Basically the range of possibilities is between 0 (which means no threshold should be used) and 1 (which means that the reference image must be an exact pixel-for-pixel match). 

The exact values in between have no absolute meaning

For example a match that requires drastic resizing of a reference image will come out as a lower match strength than otherwise


It's recommended you try the default setting

Then incrementally **lower** the threshold if you're **not finding** matching elements

If you're matching the **wrong** element, try **increasing** the threshold value

**Note:** If you use 0 as the threshold, it appears to **always** pass the `assert.exists()` test


#### Gotcha #6 - findElementByClassName()

`findElementByClassName()` does **not** search for css class names like you might expect, but rather className like `Image` or `TextField`


#### Gotcha # 7 - findElementByAutomationText()

I tried setting automationText on an element in my view, and find it using the `findElementByAutomationText()` method but it did not work...

After looking at the source code, it looks like `findElementByAutomationText()` calls `findElementByAccessibilityId()` (this might be a bug)



This is where I switched and went to using the Appium client to help me with the rest of my testing. I will post another blog post about that shortly! Stand by! 😉


See you next time! ✌️
