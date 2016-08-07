---
layout: post
title: ASP .NET MVC Tutorial &#58 Part 3
---

This is a tutorial series showing how to get up and running with MVC. In this section we will set up the web config connection strings and connect to the database! Also, we will work on "seeding" the database.


#### Connection Strings
* If you ran the solution now, by default there would be a database on your machine created with the name of LocalDB. The connection string for that database would look like this : 
* <add name="DefaultConnection" connectionString="Data Source=(LocalDb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-DeveloperUniversity.mdf;Initial Catalog=aspnet-DeveloperUniversity;Integrated Security=True" providerName="System.Data.SqlClient" />

* But what does it mean?

* (LocalDb)\MSSQLLocalDB is the name of the SQL Server Express instance that will be created for you (It is built into Visual Studio). It is used to manage local databases for you.
* Initial Catalog is the name of our database which is **aspnet-DeveloperUniversity**

<!-- TODO:

Web.Config connection strings
Web.Config transforms
Seeding the DB -->