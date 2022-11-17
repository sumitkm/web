---
title: "Removing Linux and grub loader from a Dual boot system"
date: "2007-10-21"
categories: 
  - "os"
tags: 
  - "bootloader"
  - "dual-boot"
  - "grub"
---

There are a million posts on how to do this, but I'll still post my experience.

UPDATE: A lot of people have complained in the comments that my story is rambling and irrelevant, so before I go about it, here is the link that will give you the exact steps. You can jump to it and ignore my ramble completely.

[http://www.ntcompatible.com/How\_to\_remove\_GRUB\_loader\_t28242.html#154819](http://www.ntcompatible.com/How_to_remove_GRUB_loader_t28242.html#154819 "Opens in a new window")

If you are still with me, here is my experience.

In the early part of the 2007 I had to make my Dell Latitude 510 a dual boot. It had come with a Win2k3 installation with two HDD partitions. I had 're-done' one partition to install Redhat Linux ES 3.x. Very soon work with the Linux partition got over and I was (happily) back to using Win2K3 server, till 'Gordon Moore' struck. The old adage - 'Data will increase to occupy all space available' became a reality. Soon I was uninstalling/deleting/compressing 'things' on a weekly basis to meet increasing demands of space on the meagre 20GB partition.

The slight risk of losing all data (most of which was already in the source control) had kept me from experimenting, but finally I got fed up. Today I decided I was going to take the risk.

After 5 minutes of googling it was clear that removing the Linux partition wasn't such a big deal, but the GRUB loader wouldn't go down easily.

First I tried a method that I had opted ages ago, try removing the linux partitions using the linux 'fdisk' utility. Unfortunately I didn't have the Red Hat installers, but I did have a Fedora 7 ISO. Burnt it on a DVD and booted up with it. Tried all options presented but couldn't make it to the 'fdisk' menu. Kept saying driver ISOes not found. Gave up after 4 attempts.

Fact that I had forgotten the root password of the Linux setup also didn't help.

Booted up Windows, went to Control Panel->Administrative Tools->Computer Management->Storage Management.

All the partitions (Linux Primary/Swap and of course Windows) partitions were visible. The Linux partitions were ofcourse marked unrecognized. Deleted the linux partitions and created a logical drive on the resulting 'Unallocated Space'

Still had a "Primary EISA" partition of about 47 MB. This was Sitting in front (to the left in the GUI) of the C partition. Did not mess with it. 47MB was not worth losing all data.

Formatted the new Logical drive.

After contemplating for about 5 minutes of whether to mark the C: partition as "Active Partition" or not I decided to bite the bullet. Windows help only mentioned which partitions can be "Active". It didn't say what would happen if you made it active. I did it, under the incorrect assumption that it would fix the MBR and get rid of GRUB, because googling made it clear that **fdisk _/mbr_** was NOT the thing to do in a win2k3 setup.

With crossed fingers I rebooted...

SPLAT!!!

GRUB threw up on my face. Instead of the familiar boot menu all I got was

grub>

Now what???

Run to the desktop computer and google again. Someone had mentioned fixmbr from a recovery console. Also dug out the Win2K3 setup disk. Inserted it and booted (boot sequence is CD->HDD1->USb1). Went into the Windows Recovery Console.

It detected the Windows installation correctly and asked me to select which installation to recover. First time around I just hit Enter, only to realize that it will reboot if you don't provide it with the 'number' of the partitions it detected. Next time type 1 and then 'Enter'.

Reached

**C:\\Windows**

This link gave exact sequence of steps to recover MBR

[http://www.ntcompatible.com/How\_to\_remove\_GRUB\_loader\_t28242.html#154819](http://www.ntcompatible.com/How_to_remove_GRUB_loader_t28242.html#154819)

The only thing it didn't mention was the scary messages each of those commands would throw up. Anyway, after wading thru threat of doomsday the last command **bootcfg _/rebuild_** took the longest (about 5 minutes). In the end it wanted to know what should the partition be identified, I entered "Windows2003 Server", next it asked to enter "Boot Options" for which I just hit "Enter" and finally it was supposedly done.

Again crossed fingers and **C:\\>Exit**

Came up with a BootMenu that had two options "Windows2003 Server" and "Windows 2003 Server Standard". I was expecting this because it is mentioned as a side-effect in one of the posts in the same discussion above.

Couldn't wait to hit enter for the default option and Windows 2003 server booted up... Phew!!! Still to cleanup the bootconfig file to remove the extra boot option, but otherwise, things are nice an fine now.

All this to recover 14GB of HDD space. Sigh!!!
