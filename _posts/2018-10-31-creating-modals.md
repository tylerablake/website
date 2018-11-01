---
layout: post
title: "Creating Modals"
excerpt_separator: "<!--more-->"
categories:
  - NativeScript
tags:
  - Intro
  - Overview 
  - NativeScript 
last_modified_at: 2018-10-31T11:30:00-00:00
---


Sometimes you don't want to clutter a single page with a bunch of inputs, lets see how to use modals to help with this!
<!--more-->

One of the primary focuses for software is to collect user data, on mobile devices we have to be considerate of our users and make data entry easier for them. 

Sometimes we have to collect a lot of data so a common way to make this more pleasant for the user is to use modals.

In this example I want to collect a date input from a user but I want to use a modal to show the DatePicker component.

## First we need to create our initial form

This is the page that will trigger the modal form and where we will return to after the modal action has completed. 

For this I have a basic `Label` and `TextField` which contains an tap event like so `(tap)="onDateTap()"` 

<!-- ![Base Modal Form]({{site.url}}/assets/images/base-modal-form.png){:class="img-responsive"} -->

<img src="{{site.url}}/assets/images/base-modal-form.png" class="img-responsive" height="300" width="300">

## Now we have to create that `onDateTap()` function

Here is all of the code for the base form. I have highlighted the `onDateTap()` function.

![Base Form Code]({{site.url}}/assets/images/base-form-code.png){:class="img-responsive"}

The most important part here is:

`context: this.date == null ? new Date() : this.date,`

This means we are going to pass `this.date` to the modal to be set inside of the modal view. 

This is primarily for when a user wants to update the date, when we display the modal we want to display the value previously set for that field.

Then when the modal is closed, the value isreturned to us as `dialogResult` later in this function.

## Now we have to create the modal

Modals are nothing more than just another page with a form, the only trick is that we have to pass the data between the initial form and the modal form, and visa versa. Let's look at how that happens.

<img src="{{site.url}}/assets/images/modal-example.png" class="img-responsive" height="300" width="300">

Right now the modal is nothing more than a `StackLayout` with a `DatePicker` and a `Button`.

![Modal View Code]({{site.url}}/assets/images/modal-view-code.png){:class="img-responsive"}

Now let's look at the component code for this modal.

![Modal Component Code]({{site.url}}/assets/images/modal-component-code.png){:class="img-responsive"}

The important line in this component is this: 

`this.date = params.context;`

That line sets the DatepickerModalComponent's `date` property to the date we passed through the `context` property previously.

After you set the date, we need to return to the intial form, all we have to do is set up the `onDoneTap()` function which has the following code:

`this.params.closeCallback(this.date);`

All that does is close the modal dialog and returns `this.date` which is the updated value

## Retrieving the modal data

Now we need to return to the initial form and update the date `TextField` we had there

![Returning Data From Modal]({{site.url}}/assets/images/returning-data-from-modal.png){:class="img-responsive"}

And since we had the `TextField` one way binded to the date property on the component like so:

`[text]="date | date:'shortDate'"`

We see this after hitting done on the modal page

<img src="{{site.url}}/assets/images/updated-base-modal-form.png" class="img-responsive" height="300" width="300">

Now you know to to create modals to make user input more pleasant.

Don't forget that you can use a modal for any data entry, it doesn't have to be a `DatePicker`. 

**Note: You can only have 1 modal open at a time. You can not open 1 modal which opens a 2nd modal, you must close each modal before opening another one.**

If you have any questions or comments feel free to leave them below and as always, stop by and check out the [NativeScript Docs](http://docs.nativescript.org "NativeScript Docs Link") :)
