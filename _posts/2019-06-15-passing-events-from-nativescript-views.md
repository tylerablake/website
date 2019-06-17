---
layout: post
title: "Passing Events from NativeScript Views"
excerpt_separator: "<!--more-->"
categories:
  - NativeScript
tags:
  - Overview 
  - NativeScript 
last_modified_at: 2019-06-15T19:30:00-00:00
---

Today I'm going to show how to pass event data to the code behind from the view in NativeScript and modify the widget
<!--more-->

Here's what I am going to show you today

![Blog Preview Gif]({{site.url}}/assets/images/pass-event-blog-preview.gif)



**Note:** My example will show how to do this using a button but it can be done with any UI widget.

## Set Up the View

Inside of your `component.html` file add the following: 

```
<StackLayout>
 <Button text="Tap me" class="btn btn-primary" (tap)="onButtonTap($event)"></Button>   
</StackLayout>
```

You may have seen this around and wonder what is **$event**?

To put it simply, it is an `event`, in this case the event is a `tap` event.

## Set Up the Tap Method

Now we need to set up the `onButtonTap()` method in our `component.ts` file.

You might have seen `$event` passed to the code behind method like so `onButtonTap(args)` but since this isn't typed, you won't get any intellisense help.

Let's set up our `onButtonTap()` method like this:

```
onButtonTap(args: EventData): void {    
    // We'll fill this out next
}
```

**Note:** Add this import to the top of your `component.ts` file: 

`import { EventData } from "tns-core-modules/ui/page/page";`


Now let's fill out that method and update the button from the `component.ts` file

First, we need to get a reference to the button, lets take a look at `args` which is typed as `EventData`

This means it has 2 properies on it:

1. **eventName** - string which is the name of the event
2. **object** - Observable object


We can use that `object` property to get a reference to the button in the view.


Update your `onButtonTap()` method to look like this: 

```
onButtonTap(args: EventData): void {
    const button = <Button>args.object;        
}
```

**Note:** Add this import to the top of your `component.ts` file: 

`import { Button } from "tns-core-modules/ui/button";`


Now if you type `button.` you will see a big list of properties and methods you can call on that `Button`

![Button Intellisense Dropdown]({{site.url}}/assets/images/button-intellisense-dropdown.png){:class="img-responsive"}



Let's change the background color to red and update its text after tapping on the button by adding the following line:

```
onButtonTap(args: EventData): void {
    const button = <Button>args.object;   

    //Add These 
    button.backgroundColor = "red";
    button.text = "You tapped me!";
}
```


Now when the app launches it will be a blue button, but after tapping the button will change to red.

**Before Tapping**


![Button Before Tap]({{site.url}}/assets/images/button-before-tap.png){:class="img-responsive"}



**After Tapping**


![Button After Tap]({{site.url}}/assets/images/button-after-tap.png){:class="img-responsive"}

Hope this helps you out on your app!


See you next time! :)