---
layout: post
title: "Understanding Grid Layouts"
excerpt_separator: "<!--more-->"
categories:
  - NativeScript
tags:
  - Intro
  - Overview 
  - NativeScript 
last_modified_at: 2018-07-03T12:43:00-00:00
---


NativeScript has many different layouts, let's dig into grid layouts for a few.
<!--more-->


## Basic Grids

Here is an example of a **1x3**  grid layout:

![Example 1x3 Grid]({{site.url}}/assets/images/example1x3Grid.png){:class="img-responsive"}


Here is an example of a **2x3**  grid layout:

![Example 2x3 Grid]({{site.url}}/assets/images/example2x3Grid.png){:class="img-responsive"}

### Recap:

A **GridLayout** is just that, you have columns and rows. In the 2x3 grid layout, we are telling NativeScript that we want it to generate a grid that has 2 columns and 3 rows. After you populate the **rows** and **columns** attributes of the GridLayout, you have to tell the elements within the GridLayout where they should be positioned within the grid through the **col** and **row** attributes.


GridLayout row and column definitions are **zero based**. This means row="0" actually refers to the first row in the grid.

You can make a GridLayout have as many rows/columns as you like/need.


## RowSpan and ColSpan

Here is an example using the rowSpan attribute:

![Example RowSpan Grid]({{site.url}}/assets/images/rowSpan.png){:class="img-responsive"}

Notice how we told it to make the orange StackLayout in column 1 row 0 to span 3 rows, in this instance it will span the entire grid since it only has 3 rows.


Now lets see what happens when you use both the rowSpan and colSpan attributes:

![Example RowSpan and ColSpan Grid]({{site.url}}/assets/images/colSpanAndRowSpan.png){:class="img-responsive"}

### Recap: 
In this example we told the orange StackLayout to span 2 rows instead of 3 which will make it span 2 out of 3 rows in the GridLayout this time. We also made the green StackLayout span 2 columns which will make it span the entire width.


## What does * do?

Setting a row or column to * makes it take up the rest of the space available. If you use row="*,*" then you will get 2 rows, 1 takes up the top 50% of the space available, the other takes up the bottom 50%. Here is an example:

![Example Grid using stars]({{site.url}}/assets/images/usingStars.png){:class="img-responsive"}

### Recap:
In this example we made a grid with 2 columns, one with a defined size of 50, the other is *. We have 3 rows, two with a defined size of 100, and the last is *. We can see that the manual defined size rows/columns are generated and the row and column with * size stretch the rest of the space available.

## Explicit Row and Column Sizes

In the last example we manually defined some column and row sizes in the GridLayout instead of just using *. Here is another example of that:

![Example RowSpan and ColSpan Grid]({{site.url}}/assets/images/usingManualWidths.png){:class="img-responsive"}

### Recap:
Here we can see that the rows are evenly divideded upon the space available. However, the columns are not. The first column is 100 pixels wide, and the second is 300 pixels wide. This can come in handy when you have very specific requirements or needs for your GridLayout.


## What about Auto?

Using the auto value for a column or width will have the row or column take up as much space is needed. Lets see that in action:

![Example Auto and Star Grid]({{site.url}}/assets/images/autoAndStar.png){:class="img-responsive"}

### Recap:
Here we have a GridLayout with 1 row and 2 columns. The columns are defined with columns="auto,*" inside the GridLayout. We know that the * means the second column will stretch the rest of the space available. The auto value means that the first column will use as much space as it needs. Since we gave that StackLayout a width of 50 pixels, the first column will only take up 50 pixels.


Now you can go create all kinds of cool GridLayouts!



More blog posts **are coming** but in the meantime, stop by the [NativeScript Docs](http://docs.nativescript.org "NativeScript Docs Link") to learn more!