---
author: "Sumit"
title: "Dual Booting LINUX (Debian Jessie) and OSX (Yosemite)"
date: "2015-09-10"
categories: 
  - "linux"
  - "os"
tags: 
  - "debian"
  - "jessie"
---

Back in my college days (aka... once upon a time, very long time ago) Linux installation used to conjure up pictures of geeks sitting amidst a forest of cables, wires and exposed h/w parts, peering into consoles with green text (been there, done that). Well, if you still think the same, you are in for a surprise with any of the contemporary Linux distributions today. They are just as neat, efficient and functional as any of the commercial OS vendors (snicker snicker ![Winking smile](images/wlemoticon-winkingsmile.png)). Today I am going to try and document what I did to get Debian Jessie on my MBP alongside OSX.

## Starting off

To start off with I already had a Windows partition along with OSX Yosemite. I had used Bootcamp's regular instructions at the time so nothing special.

Step 1: Create a Windows partition with Bootcamp.  
Step 1a (Optional): Mentioning it because I had Windows 10 installed, so you can install some version of Windows. But if you don't I am assuming it will be fine.

Step 2: Download the latest CD for Debian, I used Jessie because that's the current release for AMD64/x86 Architecture.

Step 3: Download Rufus the Bootable USB creation tool. In the past I have used the Windows USB tool but now-a-days ISO images come in multiple formats that the dumb USB tool can't interpret. So Rufus! (Yes, I used Rufus on a Windows machine, if you are OSX only you can use a suitable tool e.g. [https://launchpad.net/ubuntuusbcreator-osx](https://launchpad.net/ubuntuusbcreator-osx "https://launchpad.net/ubuntuusbcreator-osx") not used it myself so not sure of effectiveness).

Step 4: Plug in a suitable USB stick and ask Rufus to create a Bootable USB for you (MBR/FAT32). Once done shut down the MBP, plug in the USB stick (in case you used a different machine to create it).

Step 6: Press the power button while holding the Option key on the MBP's keyboard. This should bring up the boot menu that will present a bright orange image of a USB stick as EFI boot. Select it and you should be presented with Debian's installation menu.

Step 7: Select 'Install Debian' to start installation process. I don't have images of each step, but roughly there is the sequence:  
a. Select Type of Install - Graphical or Text Based (Text Based simply means ASCI GUI instead of a Windowed GUI. You don't have to type in commands on a green terminal at any point. (I chose Text Based)  
b. Select Language and Keyboard Layout  
c. You can choose to not provide a root password and simple create a user account with strong password. The installation will add this user to the sudoers list automatically. This will disable the root account though.  
d. NOTE: Step d and e may be swapped in sequence of events, I don't remember exactly. At this point it tries to access Wifi and since Broadcomm's Wifi chipset in my MBP (ymmv) doesn't have a driver bundled, the installer gives you the option of getting the driver separately and providing it. I simply skipped it because my laptop was plugged into the wired network. Having a live internet connection is really the key to a smooth install. Once the network drivers were installed and network connection established you are nearly ready to fly.  
e. Next comes the critical step of disk partitions.

Step 8: Partitioning the drive - Debian gives you options of Automatic Install, Manual Install and Overwrite entire disk with a couple of options.  
If you select Automatic partition it will first try to see if you have free un-partitioned space. If you don't have a Windows installation it will find this unpartitioned Free Space and ask you proceed (select the defaults and proceed).

However, if you have a Windows Partition already, you'll HAVE to select the Manual Install.  
Assuming you only one SSD/HDD you'll see it as sda (0,0,0) and you should see another reference to the USB drive.  
\- On sda(0,0,0) you'll see either one or two HFS+ partitions depending on whether OSX installation created a recovery partition or not.  
\- The other partition should each be the Windows Partition. Select this and erase it. Once it is done, you will again see it as Free space. Select it and say use this partition. The installer will ask you how to you want to partition it, select the default and you'll be fine. Once done you are ready to go.

e. The installer will ask you the nearest mirror to get updates from. Select appropriately and off you go.  
f. I had around 1400+ updates that were downloaded and installed in about 35 minutes (ymmv depending on your internet speed).  
g. You will be given the option to select your XWindow environment, I chose Cinnamon, you can chose between KDE, GNOME and a few more options.

g. Once installation completes you will see the installer setting up GRUB bootloader (I got version 2.02 Beta2-22). Once GRUB finishes, the installer will as you to unplug the USB drive and shutdown the system.

## Powering up to Linux

Next time you power up, you will see the GRUB menu. Don't panic, your precious OSX installation hasn't vanished. If you want OSX press the Option key when powering up and you can boot into OSX again. There you go, all set to play with the Penguin on your Fruity laptop.

## Looking Back...

About 4 months ago I had tried my last attempt at breathing new life into my dated 2009 MBP by installing a brand new 500Gig Crucial SSD in it. While installing OSX Yosemite wasn't a problem in the first 250Gigs. The experiment with Windows 10 (started with technical previews) in the other 250 went horribly wrong. Long story short, Windows 10 simply was too painful to use on the laptop. I had hopes of things improving after Windows 10 RTM-ed but no luck. Eventually I decided time had come to try something else. Since I was going to Raspberry Pi work on the side, I thought it would be a good idea to try Debian on full blown desktop environments. Lets see how this experiment goes.
