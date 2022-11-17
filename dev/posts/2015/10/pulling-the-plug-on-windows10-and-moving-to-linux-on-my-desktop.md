---
title: "Pulling the plug (on Windows10) and moving to Linux on my desktop"
date: "2015-10-13"
categories: 
  - "linux"
  - "os"
tags: 
  - "debian"
  - "jessie"
---

If you have followed my [recent posts](https://sumitmaitra.wordpress.com/category/all-articles/os/linux/), you know I am working on this experiment on what it takes to wean myself off non Open Source OSes. Over the past weekend I decided it was time to walk the talk and pull the plug on Windows 10 on my Desktop. To be honest, it is not possible for me to avoid Windows 10 because my current Dev platform at work is heavily dependent on Windows (and Visual Studio), but the experiment is to see if I can avoid using Windows/OSX when not working and for my hobbies. So far there are some glaring gaps in my requirements (that I know have solutions but), I used to skirt them by going back to Windows, so I decided lets pull the plug and then figure out how to solve those issues. So here's how I went about it.

# Virtualizing current Windows system

I wanted to convert my current desktop into a VM and then pave the machine to run Debian Jessie. Luckily I have two Disks – a 250 Gig SSD for OS and software and a 1TB HDD. This makes things really easy. If you don't have a second disk, have a spare external disk with lots of free space.

## Using Disk2vhd to create VHDs out of your current Windows system

Turns out Microsoft (Sysinternals) has a fabulous little utility called [Disk2vhd](https://technet.microsoft.com/en-us/library/ee656415.aspx).

Download it-> run it -> point it to the Disks that you want to convert to VDHs and provide an output folder. Default output folder is where you are running the util from.

I planned to created Virtual Box VM out of my VHDs, but it supports VHDX only in readonly mode, so I unchecked the 'VHDX' option in Disk2Vhd before I initiated the creation so that I can use the VHD directly in Virtual Box on Linux.

Note: If you used the D: of your system for storing files it's worth including it in the VHD. I made the mistake of not including it, and as a result later with Windows started up, it was iffy about OneDrive, because I had moved all my account folders to the D:. There is no data loss but just that you'll have to run some hoops to get the VM doing exactly as it was on the Desktop.

Once the VHD creation is complete, you are good to go. This is actually a very good way of backing Windows up, wonder why I didn't do it more often in the past. Anyway, done now.

# Installing Debian with KDE Plasma

In the past I have played around with Cinnamon as my Desktop of choice, though on the laptop I installed Cinnamon and KDE. In such a setup Cinnamon was the default but it had KDE apps around. This time I wanted to go all KDE and see their Plasma desktop in action. So I installed KDE only when asked for choice of Desktops.

When I logged in the first time I was very impressed with how smooth the Desktop experience was. It has elements of Windows, OSX and Gnome in it, but it is really really refreshing.

Cinnamon supports all the Windows shortcuts by default like WinKey to bring up Start Menu, WinKey + E for File Explorer and so on. KDE seems to need a bit tweaking to get it to work like Windows, maybe it has OSX keys by default, not sure. Anyway, I was easily able to support Winkey + Left or Winkey + Right for window align and WinKey + R for bringing up the Application Search. WinKey doesn't bring up anything on its own though (yet).

Though Konqueror is the default Browser on KDE, I setup IceWeasel (Firefox for Debian) as my default.

I think I like Plasma, but time will tell if it's just the new fangled toy syndrome or if it will actually help be more efficent than Windows or OSX.

# Restoring Windows and a major SNAFU

Once I got Debian going I set it up using the steps in my previous posts. That went smooth.

I followed the official Debian documentation to install VirtualBox.

On VirtualBox I created a new VM and selected '64Bit Windows 8.1' and pointed it to the VHD I had created using Disk2Vhd earlier. (I did make a copy of the original VHD knowing its the only way to get back my Windows Machine if anything went south). I had to give the VM 8 Gigs of RAM and selected ICH9 chipset for Windows to recognize the Sound Card correctly.

However after Windows 10 re-initialized itself and came back, it refused to activate saying the ID had been blocked. Now I didn't put in a Key for Windows 10 specifically, I had upgraded from Windows 8.1. But Windows kept refusing to recognize the 8.1 Key. So currently I have a working VM that's not activated. This possible means I'll have to repave the entire machine and go back to Windows 8.1 (which wouldn't be so bad actually). But that's for another day. This is just a heads up, Microsoft doesn't really want you to move your Windows license anywhere other than where its installed even if it happens to be the same machine where you had it initially. This is the type … oh well, I promised myself I wouldn't rant, so stop.

# Replacing OneDrive

A cloud synced storage platform is the only thing I need to do my work efficiently. While I could easily use DropBox as a paid replacement for OneDrive, I lost bit of faith in DropBox with their policy changes in the past.

So I am working on a little project of my own that allows me to maintain a cloud repository of important files (mostly pictures of scenery I capture ;-)...) . It's tentatively called KalliopeSync and uses Azure (I know about the irony) Blob storage at the moment.

The cost of using Azure Blob Storage for my files is less than to cost of a latte per month. So I tell myself on a random day of the month, that today I am paying for my cloud storage and skip the latte ;-). There you go, free cloud storage :-) :-) :-).

It adds to my long list of personal projects, and yes, this [CommitStrip](http://www.commitstrip.com/en/2014/11/25/west-side-project-story/) is meant for me, but hey, its the idea that counts... or maybe not, whatever!

# Looking ahead

I am hoping, by forcing myself to move out of my comfort zone I will be able to explore Linux more and help me expand my toolbox of Web Development tools/technologies and platforms.

I don't hate Microsoft or anything, just that with Windows 10 we've come to an ideological crossroad that forces me to take the path less traversed. If Windows ever came with a “Leave me alone” button that, in a single click, transferred ownership of my computer and data back to me, I would happily pay for it and use it. Till such time ...

P.S. I will miss Live Writer... hope it gets open-sourced some day...
