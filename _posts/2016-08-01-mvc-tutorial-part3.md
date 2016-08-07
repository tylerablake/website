---
layout: post
title: ASP .NET MVC Tutorial &#58 Part 3
---

This is a tutorial series showing how to get up and running with MVC. In this section we will set up the web config connection strings and connect to the database! Also, we will work on "seeding" the database.


#### Connection Strings
* If you ran the solution now, by default there would be a database on your machine created with the name of LocalDB. The connection string for that database would look like this 

<img src="/assets/localDBConnectionString.png" width="300px;" height="30px;" style="margin:auto;">

* But what does it mean?

* (LocalDb)\MSSQLLocalDB is the name of the SQL Server Express instance that will be created for you (It is built into Visual Studio). It is used to manage local databases for you.
* Initial Catalog is the name of our database which is **aspnet-DeveloperUniversity**


#### Transforms
* LocalDB instances of our databases are great for simple practice applications, but are not very practical for real world applications.

* Sometimes we would like to use LocalDB for debugging in our development environment but connect to a customer's database in production or release. This is where transforms come to the rescue!

* Transforms are used in Web.Config files to tell the solution how to act depending on the environment that the solution is deployed.

* Below you can see that we have set some properties on our **Release** connection string. We gave it an **xdt.Locator** and **xdt.Transform**

<img src="/assets/transformAttributes.png" width="300px;" height="30px;" style="margin:auto;">

* The transform property tells the solution that we want to set the attributes.
* The Locator property tells the solution what part of the web.Config file we are looking to modify.

* This is all we must do to get the functionality we wanted, but there is 1 thing we must make sure of. The **Name** property of the connection strings **must must**. (Shown below)

<img src="/assets/localDBConnectionString.png" width="300px;" height="30px;" style="margin:auto;">
<img src="/assets/releaseConnectionString.png" width="300px;" height="30px;" style="margin:auto;">

<!-- TODO:

Web.Config connection strings
Web.Config transforms
Seeding the DB -->