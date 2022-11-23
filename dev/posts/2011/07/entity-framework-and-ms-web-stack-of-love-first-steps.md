---
title: "Entity Framework and MS Web Stack of Love - First Steps"
date: "2011-07-14"
categories: 
  - "net"
  - "asp-net"
tags: 
  - "net"
  - "c"
  - "does-not-inherit"
  - "ef"
  - "ef-4-1"
  - "entity-framework"
  - "entityobject"
  - "magic-unicorn"
  - "modernizer"
  - "modernizer-exception"
  - "mvc"
  - "web-stack-of-love"
---

_Things they didn’t show you at MIX keynotes ![Winking smile](images/wlemoticon-winkingsmile.png)_ 

Okay, so you saw the MIX keynotes and were really really impressed with what MVC, EF 4.1 Code First and Scaffolding could do for you and excitedly sat down to try and get your old lumbering enterprise app transformed using the Web Stack of Love. Couple of steps in and you start stumbling around. Visual Studio throws errors, things stop working and you are scratching your head as to where you went wrong! Well happened to me and I got lucky in finding the solutions quickly with help from the community. Here are the details.

## Model First or Database First with EF 4.1

As mentioned above the first thing I tried to do was get my old lumbering enterprise app moved to the new MVC platform. Now when you have an enterprise platform you can’t throw it away with the accumulated data of last 5 years. So the easiest way is to go Database first, reverse engineer the database to generate your data model. Below are the steps you would follow

- Create an ASP.NET MVC Web Application using the new project template
- Create a generic Class library project
- Add ADO.NET Entity Data Model file (edmx) to the class library
- Generate model from DB Connection by connecting to the database. So far so good, no issues.
- Now you add reference to your database project to the web project, copy the connection string over from the class library’s app.config to web app’s web.config, and build it. Everything builds fine.
- You right click on the Controller folder and select Add Controller and the MVC tooling wizard comes up. You select your root entity name and ask it to generate the controller, Visual Studio whirrs for a while and bam! Error!
    
    \--------------------------- 
    Microsoft Visual Studio  
    \--------------------------- 
    Unable to retrieve metadata for 'Your.Data.Entity'. The type 'Your.Data.Entity' was not mapped. Check that the type has not been explicitly excluded by using the Ignore method or NotMappedAttribute data annotation. Verify that the type was defined as a class, is not primitive, nested or generic, and does not inherit from EntityObject.  
    \--------------------------- 
    OK    
    \--------------------------- 
    
- So what did you miss. Well EF is all code first so the old style generation of Entities (EF < v4) fail to work. If you read the last line of the error ‘… and **does not inherit from EntityObject**’ it gives you a hint.
- What now? Manually edit everything? That would defeat the whole purpose of O-R mapping right? Well solution was provided by Julie Lerman (MS MVP) in her blog [here](http://thedatafarm.com/blog/data-access/mvc3-1-scaffolding-magic-with-database-or-model-first-not-just-code-first/). I’ll summarize here.
- Go back to EDMX file and open the EDMX designer.
- Right click and select ‘Add Code Generation Item’.
- From the ‘Add New Wizard’ select ADO.NET DBContext Generator. You’ll see it gives a Model1.tt (t4 template) name. Change the name if you want to and select Add.

[![image](images/image_thumb.png "image")](/images/blog/2011/07/images/blog/image.png)

- You will see under in the class library a node gets added with the t4 template. When you expand the node you have the C# (or VB) classes for your entities.
- Now build and re-try scaffolding the Controller and things will go through smoothly.

## Taming the SQL Compact 4.0 for Model First Development

Here is another workaround for people who want to do Model First Development. Since SQL Compact 4.0 was released out of band from Visual Studio and .NET 4.0 releases, somewhere in the tooling chain something broke. As a result, when you try to add a new Connection using Generate Database Wizard you don’t see SQL Compact 4.0. You see up to 3.5 only. So how do you get 4.0 goodness?

Refer to the selected answer from this stackoverflow.com [thread](http://http://stackoverflow.com/questions/5205280/entity-framework-4-and-sql-compact-4-how-to-generate-database/5207377#5207377)

The answer is pretty to the point so I won’t repeat it here.

### Trouble with Modernizer.js  (ver 1.7.x only on VMs)

If you run your dev environment on a VM (like VM Ware on Mac), IE9 disables hardware rendering and the modernizer.js that ships by default keeps throwing exception ‘**Microsoft JScript runtime error: Unexpected call to method or property access**’. This happens for every page and become very irritating quickly.  
Solution is to go to [www.modernizer.com](http://www.modernizer.com) and download their latest library (2.0.6 at the time of writing this). Remove the 1.7.x reference from your web application and add 2.0.x version. Voila!

That’s about it for now. I’ll put down more of my experiences as I go forward with my EF adventures. When I started this article we had only 4.1 now we have 4.2 CTP out ![Smile](images/wlemoticon-smile.png). Fast! Very Fast!
