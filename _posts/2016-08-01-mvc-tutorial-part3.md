---
layout: post
title: ASP .NET MVC Tutorial &#58 Part 3
---

This is a tutorial series showing how to get up and running with MVC. In this section we will set up the web config connection strings and connect to the database! Also, we will work on "seeding" the database.


#### Connection Strings
* If you ran the solution now, by default there would be a database on your machine created with the name of LocalDB. The connection string for that database would look like this 

<img src="/assets/localDBConnectionString.png" width="100%;" height="50px;" style="margin:auto;">

* But what does it mean?

* (LocalDb)\MSSQLLocalDB is the name of the SQL Server Express instance that will be created for you (It is built into Visual Studio). It is used to manage local databases for you.
* Initial Catalog is the name of our database which is **aspnet-DeveloperUniversity**


#### Transforms
* LocalDB instances of our databases are great for simple practice applications, but are not very practical for real world applications.

* Sometimes we would like to use LocalDB for debugging in our development environment but connect to a customer's database in production or release. This is where transforms come to the rescue!

* Transforms are used in Web.Config files to tell the solution how to act depending on the environment that the solution is deployed.

* Below you can see that we have set some properties on our **Release** connection string. We gave it an **xdt.Locator** and **xdt.Transform**

<img src="/assets/transformAttributes.png" width="400px;" height="30px;" style="margin:auto;">

* The transform property tells the solution that we want to set the attributes.
* The Locator property tells the solution what part of the web.Config file we are looking to modify.

* This is all we must do to get the functionality we wanted, but there is 1 thing we must make sure of. The **Name** property of the connection strings **must must**. (Shown below)

* LocalDB Connection String

<img src="/assets/localDBConnectionString.png" width="100%;" height="50px;" style="margin:auto;">

* Release Connection String

<img src="/assets/releaseConnectionString.png" width="100%;" height="50px;" style="margin:auto;">

#### Connecting to LocalDB in SSMS

<img src="/assets/connectingToLocalDB.png" width="60%;" height="300px;" style="margin:auto;">

* Once you have connected to LocalDB you can open it in your object exporer and you may see your database

<img src="/assets/localDBObjectExplorer.png" width="50%;" height="150px;" style="margin:auto;">

* If you do not see your database in the object explorer this is perfectly normal, remember when we set up the DB context and piggy backed off of the IdentityContext? That context is set to not get initialized until someone tries to register a user or log into the application. 

* So let's run the application and register a user 

**Note**: you may notice that once you enter credentials the application takes longer than normal to load. This is because the proejct is creating and seeding your database for you.

* Now once your application loads you can go back to SSMS and refresh the object explorer window and you will now see your database, but it will be empty because we haven't configured any seeding of our database. So let's do this now!


#### Seeding the Database

* Setting up your project to seed your database for you will help you in your development environment for debugging purposes without having to run through parts of your application manually to get data into your database.

* MVC projects automatically scaffold some sample code for you in the Seed() method so where and how to seed the database are already written out for you!

<!-- * Default Seed Method

<img src="/assets/defaultSeedmethod.png" width="60%;" height="50px;" style="margin:auto;">
 -->
<!-- * Updated Seed Method

<img src="/assets/defaultSeedmethod.png" width="60%;" height="50px;" style="margin:auto;">
 -->

* Now that we have that done, let's blow away our DeveloperUniveristy database and close connections and run the solution 

* To do this right click on "Developer University" in the object explorer and click "Delete". Then make sure to check "Close Existing Connections" then click "Ok".

<img src="/assets/deleteDatabasePrompt.png" width="100%;" height="500px;" style="margin:auto;">

* Most likely the tables have been generated but are still empty, lets run the **Update-Database** command in the **Package Manager Console**. As shown below, this will cause the seed method to fire immediately.

<img src="/assets/updateDatabaseCommand.png" width="80%;" height="100px;" style="margin:auto;">

* Now your database should be seeded with test data.


 
<!-- TODO:
Seeding the DB 
-->