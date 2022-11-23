---
author: "Sumit"
title: "QuickBytes: Visual Studio 2013 refuses to load some projects from a VS2010 solution"
date: "2013-11-07"
categories: 
  - "asp-net"
  - "quickbytes"
  - "visual-studio"
tags: 
  - "nuget"
  - "package-restore"
  - "vs2010"
  - "vs2013"
---

Last night I opened an ASP.NET MVC project in Visual Studio 2013 that was originally created in Visual Studio 2010 and found that 4 of the six projects in the solution were not loading. This solution was working in VS 2012 earlier so I was wondering what went wrong!

After goofing around I found the Output Window (the Window menu has been split up and moved around in VS2013 – It’s at Debug->Windows->Output; _Who moved my cheese!!!)._ On selecting Solution from the ‘Show output from’ dropdown, I saw one such error for each project that was not loaded:

C:\\Users\\SKM\\Documents\\My Projects\\\[redacted\].csproj : error  : The imported project "C:\\Users\\SKM\\Documents\\My Projects\\\[redacted\]\\.nuget\\nuget.targets" was not found. Confirm that the path in the <Import> declaration is correct, and that the file exists on disk.  C:\\Users\\SKM\\Documents\\My Projects\\\[redacted\].csproj

That’s when it struck me the code dump was created using the Visual Studio Extension SolZip, which excludes the **.nuget** folder and thus Nuget Package Restore was failing. So the fix was easy:

1\. Right click on Solution  
2\. Enable Nuget Package Restore  
3\. Reload each project or save->close->and re-open solution  
4\. Restore Packages from Nuget and you are done!

This is more of a reminder for myself!
