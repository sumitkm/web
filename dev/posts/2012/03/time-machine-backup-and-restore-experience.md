---
title: "Time Machine Backup and Restore Experience"
date: "2012-03-19"
categories: 
  - "os"
  - "osx-snow-leopard"
  - "windows-7"
tags: 
  - "backup"
  - "hdd"
  - "time-machine"
  - "upgrade"
---

Sometime back, I read Scott Hanselman’s [post](http://www.hanselman.com/blog/BACKUPYOURCRAPMissingOperatingSystemBackupsDiskImagesHomeServersBootRecBootMgrRebuildBCDFixBootAndProblemsPlural.aspx) on how meticulous he is about it backup strategy. That kind of meticulousness ensures you don’t ever lose any data whatsoever and you downtime in case of disaster is a minimum. Well, today I realized that Backups can help you with upgrades as well. So I am going to share how my backup strategy helped me upgrade my Hard disk without any Software Reinstall. A little bit of background first (or you can jump straight to the Upgrade).

## Your System Environment

I do most of my development work on Windows 7 but I run all of them on VMWare VMs running on my MacBook Pro (OSX Snow Leopard). All the VMs are stored on another external 500Gb GoFlex drive. So easiest backup strategy for a VM is to simply copy the VMWare’s VM file periodically and you are done.

That strategy didn’t work very well when my Visual Studio got corrupted. I didn’t have anything to roll back to, so I had to create a new VM all together.

##### Take VM Snapshots

Moral from the corrupt Visual Studio story was to use the VM Snapshot functionality. That’s what I did when I created my new VM. Took a snapshot at significant steps of the installation process, like OS Install, Service Pack Install, Visual Studio Install, SQL Server Install etc.

Now I haven’t had a chance to test this backup strategy, yet, but I am hoping if my Visual Studio ever get’s corrupted, one of those snapshots will come to rescue.

##### Why not use Restore Points

I like to keep my VMs small about 60Gigs each, creating restore points would mean adding more diskspace to each VM. Also Restore point is too integral a part of Windows to help if some of the windows components got corrupted. Instead Windows Backup may be a better idea.

##### Use Source control, even for your personal code

I am a big believer in source control and I host most of my personal code on Bitbucket. So whether OSX or Windows 7 all my code is up in the cloud. You can refer to my [www.devcurry.com](http://www.devcurry.com)  article on how to use [Mercurial on Bitbucket](http://www.devcurry.com/2012/02/mercurial-on-bitbucket.html). That way anytime OS has to be abandoned, only loss in source is the part that’s not backed up in cloud.

##### Time Machine on OSX

Now though my development work is on Windows 7 rest of the stuff is on OSX, so Office, Outlook, XCode etc. all run on the host system OSX. Obviously I have a significant investment in software here. I use Apple’s built in Time Machine software and a Seagate GoFlex 500GB USB2 external drive to do Daily backups. The Time Machine setup is pretty sparse and I use a third party app called Time Machine Editor to set it to a Daily scheduled backup instead of the default hourly backup that Time Machine sets out to do if enabled.

##### Selecting things to ‘exclude’ in Time Machine

Go to System Preferences –> Time Machine and select ‘Options…’ It will give you a list where you can add folders and drives that you don’t wish to be backed up. My external drives are excluded. So by default I backup everything else.

With this backup strategy in place I make sure Time Machine runs successfully every morning.

## The Upgrade

I have been itching to upgrade my internal hard drive to 1TB so that I could host my VMs on the internal drive instead of having them run off an external drive. Was tempted to get an SSD but the high cost and failure rates so far have been a major deterrence. So instead of buying a 128GB SSD for ~$150 I bought myself a WD (WD10TPVT) 1TB for < $130 from good ol’ Amazon. This model is thicker than at 12.5 mm as opposed to the 9.5 mm for the stock drive. But it fits well in my late 2009 MacBook Pro. Your mileage may vary.

The hard drive replacement process is pretty much by the book (refer to the manual that came with your Mac), nothing there. I swapped out the 250 Gig stock Hard Drive with the new one.

Next was the restore part.

\- I started the machine and inserted the OSX CD

\- The installation process kicks off. Initially the OS won’t ‘see’ your new hard drive, because it’s not formatted. So use the Disk Utility to format and partition it. Then you can continue installing OSX (Snow Leopard in my case).

\- The point at which it asks for user name give an account name that’s different from the one you used in your old installation. This comes in handy when running the Migration Wizard.

\- Let OS install complete. Boot up and check for Software Updates. Let the Updates finish. Reboot if required.

\- Now log on and go to Applications –> Utilities –> Migration Assistant.

\- Select the Mac Hard Drive in the first page and go to next

\- Select the Time Machine hard drive in the second page. Click next.

\- Select all the backed up components including users and Click continue. It takes a little bit of time at this point. Once it is done it will ask what you want to do with the user that was backed up. In my case I had made the mistake of giving the same username and my old installation and as a result the second option ‘Replace’ was disabled. I had to back out, create another admin account, log in as that account, initiate restore then then ‘Replace’ that account from the backed up account. If you selected a different account name at the time of the fresh install, no worries, just continue. That’s it, sit back and let the restore complete. For 152GB odd of apps etc it took me about 2 hours to restore. But once it’s done almost everything is back to where it was.

#### What didn’t come through

It has been only a few hours since I completed by backup and I noticed the following:

1\. I lost all my shortcuts on the Dock. They never got restored

2\. Twitter app didn’t start on it’s own. And when it started it had lost all the accounts I was logged in for. I had to re-login every account again.

3\. Office is asking for Product Key again. After I provided it, Outlook wants to ‘Rebuild’ the database index.

UPDATE 1 (March 24, 2012):

4\. XCode recovery was also not complete. There is a very important tool that get's installed with the XCode suite. It’s a command line util called ‘purge’. This util forces OSX to garbage collect Inactive memory. Without purge I can’t be as ‘agile’ I want to be with my VMs because either VMWare or OSX doesn’t release the memory of a recently shutdown VM. So either I run purge or reboot. Without which if I try to load a new VM it will crash completely!

#### What did come through

1\. VMWare Fusion 4 works great. I am typing this on a VM that was created in the previous installation.

2\. iTunes seems to have it’s clueless indexes of my music correct.

3\. More importantly iPhoto seems to have ALL my images intact (a major part of the 150Gigs)

## Conclusion

This was my first experience of ‘restoring from backup’. Looks okay so far. Knowing that my data is pretty much where I had left it, is rather comforting. There are some minor niggles as outlined above, but they are all pretty minor compared to setting up all the software all over again.

So backup my dear friends. It will help in more than one way!
