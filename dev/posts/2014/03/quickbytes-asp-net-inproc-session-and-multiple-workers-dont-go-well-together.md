---
title: "QuickBytes: ASP.NET InProc Session and Multiple Workers (don&rsquo;t go well together)"
date: "2014-03-22"
categories: 
  - "asp-net"
  - "quickbytes"
tags: 
  - "inproc"
  - "session"
  - "timeout"
  - "worker-process"
---

Last week I hit an unusual roadblock while testing an ASP.NET MVC application. The application started behaving unpredictably and session state went haywire (returned null, flipped values etc. etc.).

Since it was happening after deployment, it was a bit of a bother to debug, but I realized it was a configuration issue more than anything else. So while digging through the web.config I discovered state management was set to **InProc**. This of course implies your session is alive as long as AppPool is alive and as soon as it is recycled your session is gone.

Still unable to see what’s wrong with **InProc** and what was possibly recycling the app pool, I decided to redeploy the same application in a new website on the same machine using a new Application Pool. Voila! Everything started working. Couldn’t repro the state corruption (state variables were going null) issue anymore.

Next we assigned the new site the existing AppPool (that was being used by the site where things were getting corrupted). The issues came back. This narrowed it down to AppPool settings issue. After a side by side comparison of the settings, we found that the **Number of Workers** was 5 for the site where things were goofing up, while the new deployment’s AppPool has the value set to 1. That’s when we struck gold.

At this point a quick search revealed how **Number of Workers** work and it was amply clear why things were going south.

## Multiple Workers, Web Garden and InProc State management

Number of Workers > 1 basically creates a ‘Web Garden’ scenario on your server where there are multiple worker processes handling requests for your site. Each worker process is essentially an instance of the same executable with independent static references and also obviously, independent state management (when state management is **InProc**). As a result of this two requests to the same server may or may not be served by the same worker process. Since state is not shared between the worker processes you are going to get unpredictable behavior when the second request goes to a different worker as compared to the first request.

This is actually correct behavior because Web Garden setup of a Web Server implies that you are managing state out of process via a reliable backing store like SQL Server. So if you don’t have an out of Proc state manager, don’t use more than one Worker Processes in your App Pool. Alternatively if you want multiple worker processes (better scaling) you have to use out of process state management.

## Reference

[http://stackoverflow.com/a/14105747/710962](http://stackoverflow.com/a/14105747/710962)
