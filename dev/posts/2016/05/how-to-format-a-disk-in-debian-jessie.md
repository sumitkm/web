---
title: "How to format a Disk in Debian Jessie"
date: "2016-05-22"
categories: 
  - "linux"
  - "os"
tags: 
  - "ext4"
  - "format"
  - "mkfs"
---

I keep forgetting how to format and label a disk on my Debian system so here's a quick note to self:

Formatting == Making a File System

Usually adding a new disk means creating a partition first and then making a file system on the partition. I will come back to the creation of partition some other day. For now I just need to format my file system.

We use fdisk to identify partition.

fdisk -l

Disk **/dev/sda**: 232.9 GiB, 250059350016 bytes, 488397168 sectors
Units: sectors of 1 \* 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x8eb2d6f9

Device     Boot     Start       End   Sectors   Size Id Type
/dev/sda1  \*         2048 468553727 468551680 223.4G 83 Linux
/dev/sda2       468555774 488396799  19841026   9.5G  5 Extended
/dev/sda5       468555776 488396799  19841024   9.5G 82 Linux swap / Solaris

Disk **/dev/sdb**: 931.5 GiB, 1000204886016 bytes, 1953525168 sectors
Units: sectors of 1 \* 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0xf8b85d91

Device     Boot Start        End    Sectors   Size Id Type
/dev/sdb1        2048 1953521663 1953519616 931.5G  7 HPFS/NTFS/exFAT

Disk **/dev/sdc**: 111.8 GiB, 120034123776 bytes, 234441648 sectors
Units: sectors of 1 \* 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x9fd1cfdb

Device     Boot Start       End   Sectors   Size Id Type

/dev/sdc1        2048 234441647 234439600 111.8G 83 Linux

As seen above the disks are /dev/sda, /dev/sdb and /dev/sdc Each of them have their own partitions

I want to 'format' the /dev/sdc drive, but I already have a partition on it, so I don't need to create a partition.

To format, I need to unmount the file system first. I did it by right clicking it on Dolphin file system manager and click the Unmount context menu. You can use the umount command as well.

Once unmounted you format it using the following

sudo mkfs.ext4 /dev/sdc1 

The above command give the following output

mke2fs 1.42.12 (29-Aug-2014)
/dev/sdc1 contains a ext3 file system labelled 'WinVM'
 last mounted on /media/sumitkm/WinVM on Sun May 22 16:13:34 2016
Proceed anyway? (y,n) y
Discarding device blocks: done
Creating filesystem with 29304950 4k blocks and 7331840 inodes
Filesystem UUID: 6fdb55c8-95f9-4591-a76e-f5b0ab85a606
Superblock backups stored on blocks:
 32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
 4096000, 7962624, 11239424, 20480000, 23887872
 
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done

Dolphin will auto mount it but it will use a big GUID as its label. To fix the label use the e2label command

First we check for existing label and it comes back blank

sudo e2label /dev/sdc1

Next, we apply the label WinVM

sudo e2label /dev/sdc1 WinVM

Next, we check the label again and confirm it is WinVM

sudo e2label /dev/sdc1

WinVM

Finally, don't forget to change owner. Since our mount point was previously defined, it will be picked up automatically as soon as you apply the label. However the ownership is changed to root. Change ownership back to owner yourself using the chown command

chown -R **sumitkm** /media/sumitkm/WinVM

Where sumitkm is the username and the folder is the mount folder.

Taa daa, you are done!

P.S. This happens to be my first post using my custom built Electron JS based blog editor for Linux and OSX. Check it out at https://github.com/sumitkm/electricedit (A how to article on Electron JS has been in the works for the last 4 months now ;-)... will see the light of the day someday)
