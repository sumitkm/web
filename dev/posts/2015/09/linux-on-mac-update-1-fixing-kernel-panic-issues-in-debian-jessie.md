---
author: "Sumit"
title: "Linux on Mac Update 1: Fixing Kernel Panic issues in Debian Jessie"
date: "2015-09-20"
categories: 
  - "linux"
  - "os"
tags: 
  - "debian"
  - "jessie"
  - "kernel"
  - "panic"
---

In my previous articles I had explained how I installed Debian Jessie on my Macbook Pro and set it up to do .NET work. I had mentioned in the same about some crashes I had encountered. At the time of writing that, the crashes had seemed one-off and manageable, but soon after things changed drastically.

I had kernel panic issues almost every 15 minutes of use.

I just couldn't figure out why. In desperation I un-installed the Broadcomm drivers for wireless. This may have helped a trifle in the sense I had crashes every 30 minutes instead of 15. Again it could be the change didn't make any difference at all.

Most searches pointed to hardware issues. I ran memtest from a bootable USB, fearing the worst, but that passed too.

Now I was getting desperate. Only other 'hardware' thing left to do was change the thermal paste on the CPU/GPU failing which, abandon Linux.

Unwilling to accept that, I continued my search and finally hit a few forums where they suggested using Nvidia drivers instead of noveau that comes with default. Thing with Nvidia drivers is that... well they are from Nvidia and hence not 'free' as in GPL compliant. But I was desperate to continue using Linux so I went ahead and installed Nvidia drivers as follows:

1\. Add the non-free repository URL to apt-get (Skipped this step actually since I already had it added while installing Broadcom drivers earlier, so if you have installed any packages from the non-free repository you don't need to do this step)

sudo nano /etc/apt/sources.list deb [http://http.debian.net/debian/](http://http.debian.net/debian/) jessie main contrib non-free

sudo apt-get update

2\. Install the following packages

sudo apt-get install nvidia-glx nvidia-kernel-dkms nvidia-xconfig nvidia-settings

3\. Setup Nvidia conf for Xorg if you have Gnome shell

sudo nvidia-xconfig

4\. Reboot

## End Result

Well it's been a couple of hours now, and the system hasn't frozen. I've done all the things I did with it earlier to see if it freezes e.g. use MonoDevelop, Run TypeScript compiler, use IceWeasel, use Terminal, put it off to sleep, close lid, reopen lid, let it go to screen saver and wake it from screensaver and it has survived it all. I am going to keep it like this for the night and install the wireless drivers in the morning. If it survives that I'll consider this issue 'resolved'.

## Minor Crib

After installing Nvidia drivers I seem to have lost screen brightness control functions via F1 and F2 buttons. Thought F5 to F12 work (keyboard backlight + multimedia and sound buttons). This would have been okay if Nvidia drivers had not came up with the brightest settings possible for the screen. Had to go into Nvidia's control panel and dial it down a few notches to stop it from burning my retina :-)

## Left on overnight...

I am very happy to report that the system ran peacefully last night. I managed to configure IceDove to get all my emails and left it on overnight. IceDove managed to get 12 years worth of email headers overnight and there was no Kernel panic. IceDove did run in a tight loop when getting emails so temperatures went soaring and the CPU Fan was hissing angrily for a long time. This nearly confirms the Kernel Panic under stress/high CPU temperatures is not 'the' issue. Up next wireless drivers (again), will update back in a few hours.

## And the wireless drivers are back...

Well, its been a few hours of running the wireless drivers. Still no issues. Though the computer has been idle most of this time. Other than trying out some themes online, I haven't done much on it. But I've never had this much stability for so long. It used to crash before this. Well then, I'll mark this issue as resolved!

Up next setting up TRIM for your SSD... I need to look this one up though, not sure you still need it in Jessie!
