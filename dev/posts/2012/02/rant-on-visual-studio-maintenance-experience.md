---
title: "Rant on Visual Studio Maintenance Experience"
date: "2012-02-25"
categories: 
  - "net"
  - "visual-studio"
tags: 
  - "mvc4"
  - "vs2010"
  - "vs2010sp1"
---

_**Warning: This is a Rant. I am waiting for my new VM to finishing patching itself. So spending time ranting here.**_

\----------- BEGIN RANT ----------

Last week, the Visual Studio team released the 2011 Beta. Unfortunately a day before that I had figured out that my VS Setup was hosed enough to not allow MVC4 beta to be installed. Now I don't usually install Beta in my dev machine but since MVC4 Beta came with a go live license and it promised to live side-by-side MVC3 I decided to go for it.

I started downloaded the complete installer and initiated the install and quickly it said that it did not find Visual Studio Installed hence couldn't continue. I was like huh WAT!?!

Naturally I turned to the venting machine also known as Twitter.

Jon Galloway from the ASP.NET team kindly responded suggesting a possible conflict. He also suggested I post it on the official forum for better response. After a few feeble attempts at uninstalling/reinstalling I posted on the Forum @ http://forums.asp.net/p/1772359/4850404.aspx/1?p=True&t=634657393972716075

I was surprised to find there was a special Visual Studio Uninstaller, but alas it was of no use.

Microsoft used to have a registry cleaner deep buried inside their TechNet site. It was like a bazooka to eliminate all registry entries for an application listed in Add Remove programs. Obviously you could  hurt yourself a lot with it (I had hurt myself once, but it had atleast ended up in me reinstalling VS only not setting up a new VM). But Microsoft got the wind of it and they have replaced it with a safer version of the software http://support.microsoft.com/kb/2438651 . Running this tool repeatedly resulted in some improvement as in the Visual Studio Installer started going to the point where it would ask which components you want to install. But hopes got dashed promptly after when it crashed saying it couldn't continue and that none of the components were installed.

After doing it for the fifth time on the third night I gave up and started building a new VM.

\---------END RANT----------

\-------- BEGIN CHALLENGE ------

Here is my challenge to the Visual Studio team. You have been known to eat your own dogfood right? Visual Studio is built on .NET. Build an XCopy Installer that does not use the Registry, period!

All your UX changes are fine. But if I have to setup a new VM every-time a minor revision is released, you are NOT optimizing for developer happiness or presenting a good developer experience.

Beta might be too late a stage to take this challenge up. But hey, here it is!

\-------- END CHALLENGE --------
