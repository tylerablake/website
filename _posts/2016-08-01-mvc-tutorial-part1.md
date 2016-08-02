---
layout: post
title: ASP .NET MVC Tutorial : Part 1
---

This is a tutorial series showing how to get up and running with MVC.

### What is MVC?

#### Introduction
* MVC is a framework containing 3 aspects, Model, View, Controller.
* **Model** : This is aspect contains your data models.
* **View** : This is the part of your application that users will see.
* **Controller** : This is where the logic behind the view will live.

#### Getting Started
* Open Visual Studio and create a new "ASP .NET Web Application" project.
<img src="/assets/createProjectPrompt.png" width="400px;" height="350px;" style="margin:auto;"> 
* Select "MVC" template and check "Add Unit Tests" if you dare :)
* By default, it will set individual account authentication for you.
* Click "Ok" and voila, your first MVC project is on its way!

#### Solution Explorer
* Now, a lot of files have been created in our solution explorer for us, but what are they?
<img src="/assets/solutionExplorerContents.png" height="400px;" style="margin:auto;"> 


#### Properties
* Here you will find assembly information about your project.
* Also, this is where the references for your project will live.

#### App Data
* App_Data is essentially a storage point for file-based data stores (as opposed to a SQL server database store for example). Some simple sites make use of it for content stored as XML for example, typically where hosting charges for a DB are expensive.

#### App_Start
* These files provide the application information regarding what the application needs to run.
* **Bundle.config** - This is where your dependent bundles are accessed such as Boostrap and jQuery.
* **Filter.config** - This is used to implement filters between users and your controllers.
* **Identity.config** - This is where all the authentication gets initialized.
* **Route.config** - Here you could set up custom routes for your application.
* **Startup.auth** - This is where the authentication for the site gets started.

#### Content
* This houses all things like CSS stylesheets, and images for your project.

#### Models
* Here is where you will place your data models for your project.

#### Views
* Here is where you will place your view code, each subfolder correlates to a controller.

#### Controllers
* Here is where the routing for your site will take place.
* You can place business logic here but I feel it is best practice to place your logic in services.

#### What about those files at the bottom?!
* **ApplicationInsights.config** - This file is used by Azure and/or IIS which are used to deploy and run your site.
* **Global.asax** - Allows you to write code that runs in response to "system level" events, such as the application starting, a session ending, an application error occuring.
* **Packages.config** - A configuration file to manage the packages in your solution.
* **Startup.cs** - A file that tells the solution what needs to be executed on launch for the application to run correctly. 
* **Web.config** - Here is where you set up configuration details for your application, such as connection strings for connecting to your database.


Now that we are aquainted with our solution explorer and files inide of it, now lets start working on our site.

#### See you in the next part of this tutorial!