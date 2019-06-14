---
layout: post
title: "Capturing Signatures with NativeScript + Angular"
excerpt_separator: "<!--more-->"
categories:
  - NativeScript
tags:
  - Overview 
  - NativeScript 
last_modified_at: 2019-05-02T14:30:00-00:00
---

Today I'm going to show you how to capture user signatures with NativeScript using the [nativescript-drawingpad](https://github.com/bradmartin/nativescript-drawingpad "nativescript-drawingpad link") plugin created by [Brad Martin](https://twitter.com/_bradmartin_ "brad martin twitter link").
<!--more-->

## Install the Plugin

Inside of your NativeScript **(v4+)** with Angular project, run the following command in your terminal

`tns plugin add nativescript-drawingpad`


## Configure the Plugin

We need to do a few things to configure the plugin for use. First we will add the UI, then configure the `component.ts` file.


## Add the UI

Add the following to your component.html file:


```
<GridLayout rows="*,auto" columns="*" backgroundColor="#FFFFFF">

    <StackLayout col="0" row="0" horizontalAlignment="center" verticalAlignment="center" backgroundColor="#FFFFFF">
        <Label [visibility]="signatureImage ? 'visible' : 'collapsed'" text="Preview" textWrap="true" horizontalAlignment="center" verticalAlignment="center"></Label>
        <Image [visibility]="signatureImage ? 'visible' : 'collapsed'" [src]="signatureImage" height="150" width="90%" borderColor="black" borderWidth="2"></Image>

        <Label text="Sign/Update below" textWrap="true" horizontalAlignment="center" verticalAlignment="center" marginTop="20"></Label>

        <DrawingPad #DrawingPad height="150" width="90%" id="drawingPad" penColor="#FF6B6B" penWidth="3" borderColor="black"
            borderWidth="2">
        </DrawingPad>
    </StackLayout>

    <GridLayout col="0" row="1" rows="auto,*" columns="*,*">
        <Button col="0" row="0" colSpan="2" text="Clear Signature" (tap)="clearMyDrawing()"></Button>

        <Button col="0" row="1" class="btn btn-primary" text="Back" (tap)="onBackTap()"></Button>
        <Button col="1" row="1" class="btn btn-primary" text="Done" (tap)="onDoneTap()"></Button>
    </GridLayout>

</GridLayout>
```

This will create a simple UI with a few buttons and a box so the user knows where to sign, it will look like this:

![Sign Here Page]({{site.url}}/assets/images/sign-here-page.png){:class="img-responsive"}


## Hook Up Code Behind

Now we need to hook up the Clear Signature and Done buttons. To do this we need to do 3 things to our component.ts file 


#### 1. Add Imports

```
import { Component, ElementRef, ViewChild } from "@angular/core";
import * as imageSourceModule from "image-source";
```


#### 2. Add Properties

```
signatureImage: imageSourceModule.ImageSource; // Image of signature
signatureImageString: string; // Base64 signature string
@ViewChild("DrawingPad") DrawingPad: ElementRef; // Reference to DrawingPad UI
```


#### 3. Add Methods


```
clearMyDrawing(args) {
    const pad = this.DrawingPad.nativeElement;
    pad.clearDrawing();
}

onDoneTap(): void {
    // get reference to the drawing pad
    const pad = this.DrawingPad.nativeElement;

    // then get the drawing (Bitmap on Android) of the drawingpad
    let drawingImage;
    pad.getDrawing().then(
        (data) => {
            console.log(data);
            if (data) {
                drawingImage = data;
                this.signatureImageString = imageSourceModule.fromNativeSource(data).toBase64String("png");
                this.params.closeCallback(this.signatureImageString);
            }
        },
        (err) => {
            console.log(err);
        }
    );

}
```

Now with any luck, we should be able to see that signature after we hit "Done".


![Signature Saved Picture]({{site.url}}/assets/images/signature-saved.png){:class="img-responsive"}

## Save the Signature

How you would like to save that signature is up to you, in the code you have both the `ImageSource` and the `base64` of the user's signature. :)


## Edit the Signature

If you'd like to edit the signature all we have to do is convert from `base64` to `ImageSource` when navigating to the page.

If you use `params` or `queryParams` to pass data from one component to another then all you have to do is update your constructor to look like this:


```
constructor(private params: ModalDialogParams) {
  // Convert base64 string signature to an Image object
  this.signatureImage = imageSourceModule.fromBase64(params.context);
}
```

Then since we added **[src]="signatureImage"** to our `component.html` file earlier, it will bind to `this.signatureImage` when the view loads.


Hope this helps you out on your app!

I tried to keep this blog post short and sweet so if you run into any issues feel free to reach out.

See you next time! :)