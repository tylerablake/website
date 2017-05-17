---
layout: post
title: Encrypting Web Config
---

Welcome! In this blog post we'll discuss how to encrypt and decrypt your web.config file.


#### Why encrypt?
* First lets talk about what a web.config file is and why we might want to encrypt it.
* A web.config file is a file that stored configuration details about your application.
* This may include session configurations, application keys (if using third party software), and database connection strings (one of the biggest reasons you want to encrypt the config file)

#### Encrypting
* Once you publish your solution to the server it will be deployed on, open command prompt and navigate to the following path.
* **Note:** This uses the regiis utility and the machine key in order to encrypt the web.config file. This prevents someone from being able to copy the web.config file to their own machine and run the command to decrypt or encrypt the file.
* c:/Windows/Microsoft .NET/Frameworks/(highest version) (currently 4.0.30319) 
* Then run this command : "aspnet_regiis.exe -pd “appSettings” -app “appName” -site “siteName"
* In this example I'm encrypting the app settings section of the web.config file, if you wanted to encrypt the connection strings you just need to enter "connectionStrings" **it is case sensitive**, instead.
* **Note:** If your site is the default site then you only need to include the app name.

#### Decrypting
* Now, maybe something in the web.config needs to be updated on the server, all you have to do is similar to the above but use **-pd** instead of **-pe**
* Once you publish your solution to the server it will be deployed on, open command prompt and navigate to the following path.
* c:/Windows/Microsoft .NET/Frameworks/(highest version) (currently 4.0.30319) 
* Then run this command : "aspnet_regiis.exe -pd “appSettings” -app “appName” -site “siteName"
* **Note:** If your site is the default site then you only need to include the app name.


