---
author: "Sumit"
title: "QuickByte: Creating a Windows bootable USB drive in Linux"
date: "2021-03-20"
categories: 
  - "all-articles"
  - "linux"
  - "os"
  - "windows-10"
---

![](https://sumitmaitra.files.wordpress.com/2021/03/images/blog/image.png?w=541)

Creating a Windows bootable USB drive in Linux

I seem to keep forgetting that creating a Windows bootable USB drive is not the same as creating a Linux bootable USB drive, given an iso image of the OS.

Usually `dd if ~/path/to/iso_file.iso of /dev/sdx BS=1M` will write out an ISO image bit by bit into a target device (USB drive).

But Microsoft can't make it all so simple right? Windows Bootable devices have three partitions, an empty 4.2MB Partition, a 524KB FAT partition and the remainder as an NTFS partition.

Instead of manually faffing around with partitions yourself, do yourself a favour and install the aptly name `woeusb` tool.

It has a command line and GUI version. Find the appropriate one. After that it is a simple command

sudo woeusb --device ~/Downloads/Win10\_20H2\_v2\_English\_x64.iso /dev/sdd --tgt-fs NTFS

Replace `/dev/sdd` with whatever your drive your USB is mounted as.

Don't forget the `target-filesystem` flag `--tgt-fs NTFS` because current Windows 10 installers are more than 4 Gigs so cannot be squeezed into a FAT file system which is the default.

I used the `Disks` utility GUI to stop the USB drive. These days most USB drives if recognised will be auto mounted, so you have to unmount/stop them before you can use `dd`.

Another issue I found was `woeusb` kept failing after creating the first partition. I forgot to capture the error message, but it would fail to create the NTFS partition and crash. You could then see the FAT partition in the `Disks` app.

This fixed itself after a reboot of my Linux box.

  
If you don't use `woesub` and wing it with `dd` only, you'll find Windows Setup will initialize, but very quickly get stuck at a screen that claims "Drivers not found" and will implore you to load up Drivers in another media. You might imagine you have to download 'Motherboard drivers' or something, but this is not correct. No amount of 'downloading drivers' will make the installation proceed. Essentially, Windows setup fails to load NTFS drivers if you don't have that FAT partition and goes round in circles looking for it.
