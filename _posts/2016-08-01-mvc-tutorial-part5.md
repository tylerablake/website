---
layout: post
title: ASP .NET MVC Tutorial &#58 Part 4
---

This is a tutorial series showing how to get up and running with MVC. Now that we have set up our solution and added our first Model, View, and Controller (scaffoleded). Now that we scaffolded the Controller, there is some refactoring we should do by implementing the use of viewmodels into that controller.. we will do that in this section.


##### What is a viewmodel?
* First lets discuss this... The model you created previously is a domain model, that is the model that gets saved to the database. It is best practice to keep that domain model near the database and that is all. So if we need to access that model in the view then what is the best way to do this? 
* Viewmodels!
* A viewmodel is a class just the same as your domain model, except you **ONLY** include properties that you want to see if the view, **AND** you do not have to set up any mapping for it.


#### Why?
* The reason you want to use these for a few reasons:
* Because it is better practice to keep your domain models away from the end users.
* It is better to pass lightweight models to and from the view, rather than passing the entire domain model
* And it helps make your application more secure and safe.
* Also with a domain model that is responsible for saving to the database and displaying data to the view violates the single responsibility prinicple but those principles are for another day. :)


#### Creating a ViewModel
* Lets create a **ViewModels** folder inside of the **Models** folder.
* Then let's add a new class and call it **EmployeeIndexViewModel**
* This is a good name because it says that this viewmodel is for the EmployeeIndex view.. which is exactly what it is for.
* Now all we have to do is add 3 properties, an integer Id, string FirstName, and string LastName.
* Here is a comparison between the Employee class and the EmployeeIndexViewModel:
<img src="/assets/employeeAndViewModelComparison.png" width="600px;" height="350px;" style="margin: auto;">


#### The Employee/Index Method/ViewModel
* Let's look at the Employee/Index method. 
* Right now the method body should look similar to this:
* "return View(db.Employees.ToList());"
* Let's say for example purposes that in the Index view, we want to show a list of Employee's first and last names with a button to edit them.
* The current method is passing a list of Employee domain objects to the view, which contians **ALL** of the employee's data which might include their address, birthday, SSN, etc. These properties we don't want to be responsible for hiding in the view and preventing end users from seeing, so lets just not send that data then right?
* All we need to do is update this method to map that list of Employees, into a list of EmployeeIndexViewModels, like shown below:
<img src="/assets/employeeIndexMethodRefactor.png" width="600px;" height="350px;" style="margin: auto;">
**Note:** You will notice that red error line under "employeeViewModels.ToList()". That is because our view is still expecting a list of Employees, but we are sending it a list of EmployeeIndexViewModels, we'll fix this in the next section.


#### The Employee/Index View
* All we need to do is open the Views/Employee/Index.cshtml file.
* Then update the top of the file to be updated like shown below:
<img src="/assets/changingViewToUseViewModel.png" width="800px;" height="150px;" style="margin: auto;">

* Congrats, you have done your first moderate refactor! Good Job.

#### See you in the next part of this tutorial!
