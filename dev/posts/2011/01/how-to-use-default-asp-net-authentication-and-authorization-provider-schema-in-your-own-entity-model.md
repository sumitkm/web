---
author: "Sumit"
title: "How to: Use default ASP.NET Authentication and Authorization Provider Schema in your own Entity Model?"
date: "2011-01-30"
categories: 
  - "net"
  - "asp-net"
tags: 
  - "aspnetdb"
  - "authentication-provider"
  - "authorization-provider"
  - "c"
  - "ef"
  - "entity-framework"
  - "postaweek2011"
---

## Background

Microsoft has provided a default authentication provider that stores usernames and passwords in a SQL Server Database. The schema and the provider come out of the box and now-a-days if you use and Web application template, Visual studio will generate all code necessary to do forms authentication and registration.

The default database for storing Authentication and Authorization mechanism is called **aspnetdb** and contains all the tables and stored procedures required.

## The Problem

You can choose to keep the default **aspnetdb** and build your application schema separately and use the provider as needed. This works fine when your own schema elements don’t need to access the roles, user or membership entities that are getting stored in **aspnetdb**. But we run into trouble if we are building our schema using the Entity Framework and want to use entities from the **aspnetdb**. Entity Designer can connect to only one database at a time. So how do we keep the out-of-the-box goodness intact, use the Entity Framework and also use the Role/membership entities in our custom entities?

## Solution

Microsoft has provided a tool for generating the entire schema in any database you want. The details are available at [http://msdn.microsoft.com/en-us/library/ms229862.aspx](http://msdn.microsoft.com/en-us/library/ms229862.aspx "http://msdn.microsoft.com/en-us/library/ms229862.aspx")

To Summarize

1\. Open “Visual Studio Command Prompt” from “Visual Studio Tools” shortcut.

2\. Type in the following commands

**C:\\Program Files (x86)\\Microsoft Visual Studio 10.0\\VC>aspnet\_regsql –d \[YourDataBaseSchemaName\] –A all –E –S \[SQLSERVER NAME\]**

The aspnet\_regsql tool has a lot of options, details for which are well documented by MS in the above link. Above I’ve used three options

\-d : Implies you are specifying a database schema where the scripts will be generated

**\[YourDataBaseSchemaName\]** **:** Replace this with the schema/database name with the one for your application

\-A : This implies Add

all : This value implies you want all the tables in your schema. There are some options to get a subset, but I just went for the whole thing

\-E : This implies you are asking it to Authenticate using current Windows Authentication for current user.

\-S: SQL Server Name. It is usually the machine name or \[machine name\]\\SQLSERVER unless you’ve named it differently yourself.

This script hardly takes a second to execute.

3\. Now the authentication infrastructure is in place. Few more steps to go:

- Change default connection string in your web.config for the provider. By default the connection string is called “ApplicationServices”. Change it such that it connects to your database.
- Open the Entity Designer, right click on the design surface and select Update Model from Database.
- Select all the tables (only) and add them to the Entity Design surface.
- Rename the **aspnet\_\*** tables as per your naming conventions. Renaming the entities doesn’t change the table names in the DB so rest assured you are not breaking anything with the default provider.

That’s it. Now you have access to the entities from the providers in your schema, feel free to use them they way you want. The default provider is intact and you get all the Entity Framework goodies for reading from the provider free of custom data layer development cost.

Have Fun!
