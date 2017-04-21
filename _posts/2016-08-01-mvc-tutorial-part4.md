---
layout: post
title: ASP .NET MVC Tutorial &#58 Part 4
---

This is a tutorial series showing how to get up and running with MVC. In this section we will discuss adding a model, controller, and views to your project.

#### Adding a Model
* Find the **Models** folder in solution explorer and right click on it. Then select Add > Class.

* Give it a meaningful name, in this instance, let's say we need to fulfill a business requirement to manage Employees. We should name this class **Employee**.

* Then we want to add a couple of properties to that class. Let's add a couple public properties: Id, FirstName, and LastName.

* **Note:** Id should be an it, so that line should look like this "public int Id {get;set;}"

* **Note:** FirstName and LastName should be strings, so they should look like this "public string FirstName {get;set;}"

* Now that we have started the creation of a new table in the database, we must inform EntityFramework about it. We'll look at that next.

* Find the IdentityModels.cs file inside of the **Models** folder. And scroll down to where the DbSet declarations for the other models are and add a new one for our **Employee** model.

* **Note:** Refer back to the screen shot under **DbContext and Mapping** section of Part 2 of the mvc tutorial if you need help finding this.

* Add a DbSet for our new **Employee** class.

* Now that we have told EntityFramework about the new table we want it to create, we have to tell it to execute those changes.

* Open PackageManagerConsole and run **Update-Database**.

* This step is required because when the app runs it tries to connect to the database and EntityFramework compares the models and properties in the solution to the tables and columns in the database.

* **Note:** If they **do not** match, then you will receive a "pending model changes error".

* Running Update-Database does the same comparison but it updates the database tables and columns to match the model classes and properties inside the solution.

#### Adding a Controller and Views

* Now we can work on scaffolding out the controller with views. Right click on the **Controllers** folder and click **Add > Controller**.

* Select **MVC 5 Controller with views, using EntityFramework**

* Inside the "Model Class" text box, enter "Employee".

* The "Data Context Class" should be "ApplicationDbContext".

* Make sure the "Generate Views" checkbox is checked.

* Make sure the "Use a layout page" checkbox is checked.

* Enter **EmployeeController** inside of the "Controller Name" text box. Then click "Add".

* When the scaffolding process is finished you will have a new **EmployeeController** file inside of your Controllers folder, as well as a new Employee folder inside of the Views folder.

* Now you should be able to navigate to "localhost:xxxx/Employee" and have CRUD functionality for employees.

#### See you in the next part of this tutorial!
