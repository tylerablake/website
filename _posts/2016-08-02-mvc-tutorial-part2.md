---
layout: post
title: ASP .NET MVC Tutorial : Part 2
---

This is a tutorial series showing how to get up and running with MVC. In this section we will discuss routes,
how an MVC application works, and start writing some code!

#### Routes
* MVC handles requests from clients through routes. You can set up custom routes through the route.config.
* Lets take a look at the default convetion for routing with MVC projects.

<img src="/assets/defaultRouteConfig.png" width="400px;" height="350px;" style="margin:auto;"> 

*Here you can see that the **Default** route for the application is:
  * Home controller
  * Index action
  * With an optional parameter (not required)


* Routing in MVC is a very important concept so lets take a closer look.
* When you navigate through your web application you can see the routing through the navigation bar.

<img src="/assets/defaultRoutingUrl.png" width="600px;" height="150px;" style="margin:auto;"> 

* Here you can see that code being executed is in the student controller, Index method.
**Note**: Index might be left off because it isn't needed in this instance, if you navigated to this page you would only see **localhost:5626/Student**

Now that you understand routing, let's start writing some code shall we?!


#### Model
* Go to the "Models" folder and create a new class, let's name it Student.cs. (We are going to write a school app).
* Let's make this class public and add a few properties.

<img src="/assets/studentClass.png" width="600px;" height="350px;" style="margin:auto;"> 

* Now you will receive a compiler error, we told the solution that our Student has a collection of Enrollments, but we haven't created that class just yet so the compiler is angry. So let's create the rest of the classes we need now.

* Add 2 more classes to the Models folder, Enrollment.cs and Course.cs.

<img src="/assets/enrollmentClass.png" width="500px;" height="400px;" style="margin:auto;">

<img src="/assets/courseClass.png" width="600px;" height="350px;" style="margin:auto;">
