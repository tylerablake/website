---
layout: post
title: ASP .NET MVC Tutorial &#58 Part 2
---

This is a tutorial series showing how to get up and running with MVC. In this section we will discuss routes,
how an MVC application works, and start writing some code!

#### Routes
* MVC handles requests from clients through routes. You can set up custom routes through the route.config.
* Lets take a look at the default convetion for routing with MVC projects.

<img src="/assets/defaultRouteConfig.png" width="600px;" height="150px;" style="margin:auto;"> 

*Here you can see that the **Default** route for the application is:
  * Home controller
  * Index action
  * With an optional parameter (not required)


* Routing in MVC is a very important concept so lets take a closer look.
* When you navigate through your web application you can see the routing through the navigation bar.

<img src="/assets/defaultRoutingUrl.png" width="300px;" height="30px;" style="margin:auto;"> 

* Here you can see that code being executed is in the student controller, Index method.
**Note**: Index might be left off because it isn't needed in this instance, if you navigated to this page you would only see **localhost:5626/Student**

Now that you understand routing, let's start writing some code shall we?!


#### Models
* Go to the "Models" folder and create a new class, let's name it Student.cs. (We are going to write a school app).
* Let's make this class public and add a few properties.

<img src="/assets/studentClass.png" width="600px;" height="350px;" style="margin:auto;"> 

* Now you will receive a compiler error, we told the solution that our Student has a collection of Enrollments, but we haven't created that class just yet so the compiler is angry. So let's create the rest of the classes we need now.

* Add 2 more classes to the Models folder, Enrollment.cs and Course.cs.

<img src="/assets/enrollmentClass.png" width="500px;" height="350px;" style="margin:auto;">

<img src="/assets/courseClass.png" width="550px;" height="250px;" style="margin:auto;">


#### Controllers
* Now we must create a controller for each of these models inside of our "Controllers" folder.

<img src="/assets/controllersSubfolders.png" width="350px;" height="150px;" style="margin:auto;">

* You will be asked how you would like the controller to be scaffolded, this means it will auto generate the controller for you based off of a data model and DbContext for you.

* **Note**: While this will write a lot of code for you, it will cause a lot of "fluff" to be generated, which means excessive code that you do not need in your controller, you've been warned. It is **best** to select "MVC 5 Controller - Empty".

#### Views

* Now that you have completed this step, you will notice that a corresponding folder has been created for you in the "Views" folder, 1 for each of the controllers you set up.

<img src="/assets/viewsSubfolder.png" width="200px;" height="150px;" style="margin:auto;">

* In each of these subfolders, you will have a file : "Index.cshtml"
* **Note**: cshtml stands for c# html.

* In these subfolders you will create a .cshtml file for each of your controller actions.
* Below you can see that I already have an Index, Create, Edit, Delete, and Details methods in my Student controller

<img src="/assets/studentViewsFolder.png" width="250px;" height="150px;" style="margin:auto;">


#### DbContext and Mapping
* You almost have a running application! But first, you must tell Entity Framework about the models you created and how to map them to your database.

* Inside of your "Models" folder, locate IdentityModels.cs, if you scroll down in this file you wil see the creation of a class named ApplicationDbContext, this is the creation of the database context for your application. 

* **Note**: You could create your DbContext class in its own file but for the sake of this tutorial we are going to piggyback on the existing ApplicationDbContext.


<img src="/assets/applicationDbContext.png" width="500px;" height="350px;" style="margin:auto;">

* Here we tell Entity Frame work how we want the Database to be created. We tell it that we want it to create 3 tables : Student, Enrollment, and Course (noted by the DbSets<> at the bottom of the file).

* Then we override the OnModelCreating method, to tell it to remove the convention to pluralize table names.

	Entity Framework by default would name the Student table, "Students", which typically is not what you want to happen, so we tell Entity Framework to remove that convention for us. 

* Now we have to tell Entity Framwork how we want the tables to be built. We told it we wanted tables for the models, but we haven't specified what relationships we want them built on. Therefore, we created a Mapping folder, and inside of it, mapping files for each of our models.

<img src="/assets/mappingFolder.png" width="200px;" height="100px;" style="margin:auto;">

<img src="/assets/studentMapping.png" width="600px;" height="300px;" style="margin:auto;">

* Since we inherited from the EntityTypeConfiguration<> class, Entity Framework will look at our mapping files as a reference on how to build the relationships for the tables for us in the database.

* Here you can see that we want a Student to have a primary key of Id, have required fields of FirstName, LastName, and EnrollmentDate, and we specify that a student may have many Enrollments. After all, what type of school only lets a student enroll in 1 course?!





