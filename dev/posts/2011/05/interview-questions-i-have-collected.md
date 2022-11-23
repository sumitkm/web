---
author: "Sumit"
title: "Interview Questions I have collected"
date: "2011-05-05"
---

Okay, I am starting this article with the intention of blogging every good/bad/ugly question I come across in interviews for a .NET Developer position. Some of them I knew the answer, some of them I look up after the interview. Aim is to have a one stop shop of questions that I’ve come across in interviews. I can’t reveal where I was asked these questions because most companies have NDA with respect to interviews and what’s discussed in the interviews so some of the questions might be really come in much later than when asked.

### ASP.NET

## 1\. What’s the difference between Server.Transfer and Response.Redirect and when and where would you use each?

Server.Transfer does not send the new URL to browser and the change in URL happens at the server end. User still gets to see the initial request URL sent.

Response.Redirect sends the new URL back to the browser and browser navigates to the new page. The URL changes for the user on the browser

Pro and Cons

Server.Transfer

\- Faster since it saves the round trip to browser

\- Initial page’s data can be transferred using the Context

\- Cannot transfer out to an external link

Reference: [http://msdn.microsoft.com/en-us/library/ms525800(VS.90).aspx](http://msdn.microsoft.com/en-us/library/ms525800(VS.90).aspx "http://msdn.microsoft.com/en-us/library/ms525800(VS.90).aspx")

_\-_ Server.Transfer cannot be called from an ASP.NET AJAX post-back because Server.Transfer returns an entirely new page where the AJAX post was expecting a partial html fragment.

Reference: [http://forums.asp.net/p/1023949/1391157.aspx](http://forums.asp.net/p/1023949/1391157.aspx "http://forums.asp.net/p/1023949/1391157.aspx")

[https://msmvps.com/blogs/luisabreu/archive/2007/10/10/no-you-cannot-call-server-transfer-on-an-asp-net-ajax-enabled-page.aspx](https://msmvps.com/blogs/luisabreu/archive/2007/10/10/no-you-cannot-call-server-transfer-on-an-asp-net-ajax-enabled-page.aspx "https://msmvps.com/blogs/luisabreu/archive/2007/10/10/no-you-cannot-call-server-transfer-on-an-asp-net-ajax-enabled-page.aspx")

Response.Redirect

\- Slower but user has actual link to the page being served.

\- First page data is not available in the second page unless transferred through query string, cookie, application state

\- Can be used to redirect to external links

Reference: [http://msdn.microsoft.com/en-us/library/ms524309.aspx](http://msdn.microsoft.com/en-us/library/ms524309.aspx "http://msdn.microsoft.com/en-us/library/ms524309.aspx")

## 2\. What’s Server.Execute and how is it different from Server.Transfer

Server.Execute is a legacy command from ASP. It executes an ASP script as it it were a part of the current page. It’s like a method call. I don’t see any resemblance to Server.Transfer which is an ASP.NET API call.

Reference: [http://msdn.microsoft.com/en-us/library/ms525849.aspx](http://msdn.microsoft.com/en-us/library/ms525849.aspx "http://msdn.microsoft.com/en-us/library/ms525849.aspx")

## 3\. How is Session state maintained between a client and server given that HTTP is stateless protocol

Session state is maintained on the server in three possible ways

InProc – Session is stored in server memory.

StateServer – Session is stored in a dedicated server on the web farm.

SQLServer – Session is stored in the SQL Server.

Custom – You could also roll your own Session state manager if required.

Excellent primer of Session state is available in the URL below.

On the client ASP.NET uses cookie by default. If cookies cannot be used you have to use URL munging and the session ID is a part of the URL.

Reference - [http://msdn.microsoft.com/en-us/library/ms178581.aspx](http://msdn.microsoft.com/en-us/library/ms178581.aspx "http://msdn.microsoft.com/en-us/library/ms178581.aspx")

[http://technet.microsoft.com/en-us/library/cc776818(WS.10).aspx](http://technet.microsoft.com/en-us/library/cc776818(WS.10).aspx "http://technet.microsoft.com/en-us/library/cc776818(WS.10).aspx")

### SQL SERVER

## 1\. What’s a clustered and non-clustered index

Clustered indexes physically sort the data. You can have only one clustered index. Non-clustered indexes are where the data is sorted logically.

## 2\. What’s the difference between Delete and Trunc

I got this ‘nearly’ right in the interview where I was asked about it, or so I thought until I found this excellent thread on stackoverflow.

[http://stackoverflow.com/questions/139630/whats-the-difference-between-truncate-and-delete-in-sql](http://stackoverflow.com/questions/139630/whats-the-difference-between-truncate-and-delete-in-sql "http://stackoverflow.com/questions/139630/whats-the-difference-between-truncate-and-delete-in-sql")

## 3\. Maximum number of columns allowed in SQL Server? (really dumb question because I don’t see the point in remembering this) because if you are needing the max number of columns in a single table something is horribly wrong with your data design!

Latest SQL Server spec sheet is as follows:

[http://msdn.microsoft.com/en-us/library/ms143432.aspx](http://msdn.microsoft.com/en-us/library/ms143432.aspx "http://msdn.microsoft.com/en-us/library/ms143432.aspx")

### Fun Stuff (The Basics)

These are some of the questions are enjoy answering debating in an interview. These have no right/wrong answer so some of them may have only what I think is the right answer

## 1\. What is Scalability in context of a web application?

Scalability is usually measured as a factor of performance at given load. Most common performance factor is response time. So if acceptable performance for response time is say 1ms-3ms; an application is deemed scalable if it is able to deliver on that performance for all load conditions. All, is again highly subjective hence more measurable criterion like requests per second should be used. So a system would be deemed scalable when it delivers on the the required response time for an acceptable number of requests-per-second. It is however deemed scalable and robust when it is pushed beyond acceptable limits and it responds gracefully by either queuing requests or reducing response time (or both). When a system crashes in face of un-chartered load it’s not deemed as a robust system.

## 2\. Given same farm configurations how would you increase scalability and performance of a web application

There is no perfect answer to this, the basic answer is Caching. As soon as you say that you will be asked how would you implement caching.

## 3\. How would you implement a size limited hashtable?

This question has it’s roots in other questions like what is a Hashtable. What’s the Big O for a hashtable lookup? What are the features of a linked list? etc. What the interviewer is looking for is your hold on basic Data Structures and thinking on your feet abilities to come up with a new data structure in the interview itself.

Well, there will be more to come in the near future, so watch out.
