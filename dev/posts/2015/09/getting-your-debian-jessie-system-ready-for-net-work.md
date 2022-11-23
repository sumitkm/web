---
author: "Sumit"
title: "Getting your Debian Jessie System Ready for .NET work"
date: "2015-09-13"
categories: 
  - "linux"
  - "os"
tags: 
  - "atom"
  - "debian"
  - "jessie"
  - "mono"
  - "monodevelop"
  - "setup"
---

As a followup to my [last post](https://sumitmaitra.wordpress.com/2015/09/10/dual-booting-linux-debian-jessie-and-osx-yosemite/ "Dual Booting LINUX (Debian Jessie) and OSX (Yosemite)") I thought I would continue with my 'learnings' on how to go about using Linux. It hasn't been all sunshine and bunny rabbits. I've had multiple crashes and one was so bad I had to re-do the entire OS installation again. I have a nagging feeling it had something to with me trying to install developer dependencies over a dodgy wifi network on the train ;-), I shall not  try that one again to confirm.  There were a couple of secondary crashes that were pretty bad too. I am close to concluding that's because my laptop's heating system is botched and I really need to take it apart and reapply the cement for better heat dissipation. Second suspect is the Broadcom wireless driver. Also the 'close lid' behaviour is a little odd as it doesn't seem to go into 'deep sleep'. It only shuts the apple logo off but its still working along silently. One day I put the laptop in the bag and took it to office, only to realize that it has somehow 'awakened' in the bag the my laptop bag was as warm as a heating pad. Now, I manually set it off to sleep before I close the lid (a little Windows XP ish, I know). I shall continue my 'investigation' and report back on progress. I am sure it's my setup somehow. Moving on, today we'll see what it takes to setup .NET on Linux (aka Mono). Before that I realized I didn't have wireless drivers. So we'll start with Wireless Driver installation.

## Setting up Wireless on OSX (2009 MBP)

1\. The wireless driver is not 'free' as per GPL licensing so it is not a part of the default installation. To use apt you have to first add a contrib component to /etc/apt/sources.list. This basically apt where to get the non-free contributions from. `sudo nano /etc/apt/sources.list deb http://http.debian.net/debian/ jessie main contrib non-free` 2\. Update packages list `sudo apt-get update` 3\. Install Broadcomm Firmware driver. Note your laptop may have different chip, notably by Atheros. To know more visit [https://wiki.debian.org/bcm43xx](https://wiki.debian.org/bcm43xx) `sudo apt-get install firmware-b43-installer` 4\. Reboot `sudo shutdown -r now` 5\. Once rebooted, the wireless devices should be listed in the system tray, just pick the one that's yours and connect to it and provide password as required. I've had a couple of crashes after installing this driver, I am not sure if I can attribute them to this driver directly. I will keep looking and update back if I find the root cause.

## Setting up Mono and MonoDevelop

As a .Net and C# geek, I need to be able to code in C# on my Linux box. So first thing to do is setup Mono and MonoDevelop. Once we have this in place we'll look at secondary tools and platforms like Atom editor and NodeJs.

1\. Goto Mono's default guide at [http://www.mono-project.com/docs/getting-started/install/linux/](http://www.mono-project.com/docs/getting-started/install/linux/) and follow the steps. Repeated here for Jessie on Macbook Pro 2. Add GPG Key `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF` 3\. Add Repository to list of sources `echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list` 4\. Update apt `sudo apt-get update` 5\. Adding mod\_mono repository to list of sources `echo "deb http://download.mono-project.com/repo/debian wheezy-apache24-compat main" | sudo tee -a /etc/apt/sources.list.d/mono-xamarin.list` 6\. Adding libgdiplus support to Debian Jessie `echo "deb http://download.mono-project.com/repo/debian wheezy-libjpeg62-compat main" | sudo tee -a /etc/apt/sources.list.d/mono-xamarin.list` 7\. Update apt again `sudo apt-get install update` 8\. Install Mono Development kit (about 155 MB) `sudo apt-get install mono-devel` 9\. Install Mono-complete (additional 77 MB) `sudo apt-get install mono-complete` 10\. Install PCL Support (Portable Libraries, additional 28.2 MB) `sudo apt-get install referenceassemblies-pcl` 11\. Install MonoDevelop `sudo apt-get install monodevelop` 12\. Install MonoDevelop NUnit plugin `sudo apt-get install monodevelop-nuit` 13\. Install Git (One would think Git comes installed with every Linux installation. While this is true for a lot of distributions, we installed from a Live CD installer, so it was the leanest installation possible). `sudo apt-get install git` 14\. Install MonoDevelop Version Control plugin `sudo apt-get install monodevelop-versioncontrol` 15\. Install MonoDevelop Database plugin. `sudo apt-get install monodevelop-database`

At the time of writing this plugin failed to install with the following error, I have ignored it for now, will revisit if I encounter a pressing need for the plugin. `Some packages could not be installed. This may mean that you have requested an impossible situation or if you are using the unstable distribution that some required packages have not yet been created or been moved out of Incoming. The following information may help to resolve the situation: The following packages have unmet dependencies: monodevelop-database : Depends: libmono-npgsql4.0-cil (>= 1.0) but it is not going to be installed Depends: libmono-system-data2.0-cil (>= 3.12.0) but it is not going to be installed Depends: monodevelop (< 5.7.0.660.) but 5.9.5.9-0xamarin1 is to be installed E: Unable to correct problems, you have held broken packages.`

At this point you are setup to create simple .NET applications – both console and MVC.

## Setting up NodeJS, PHP and the Atom Editor

The Atom editor, as defined by its creators (at Github), is a Hackable code editor that's fast becoming the goto tool as opposed to heavy IDEs like Visual Studio/MonoDevelop/IDEA/Eclipse etc. It does use Google Analytics for tracking usage and improving itself. If you are not comfortable with Google Analytics, you can disable the module (and I hope it doesn't it doesn't send anything more to Google).

### The easy way

The easy way to get Atom is to download the pre-built package from [https://atom.io/download/deb#](https://atom.io/download/deb#) and install it using `sudo dpkg -i atom-amd64.deb`

### The hackable way

The hackable way of course is to download the entire build tool chain and build it locally. There is a nice set of steps documented here [https://github.com/atom/atom/blob/master/docs/buildinstructions/linux.md](https://github.com/atom/atom/blob/master/docs/buildinstructions/linux.md) and it worked for me perfectly. It hot links to NodeJS installation instructions that are a bit redundant at the time of writing, so I'll just collate everything here: 1. Install Toolchain (note I am not re-installing git here because we did that earlier already) `sudo apt-get install build-essential libgnome-keyring-dev fakeroot` 2\. Install Node `sudo apt-get install nodejs` 3\. To avoid conflict with another package node is installed as nodejs. If you don't have the amateur radio package called Node you can setup an alternative. To first check use the following command sudo which node If this doesn't return any values, it means you are safe to setup node as the alternate command to nodejs. You can do this as follows `sudo update-alternatives --install /usr/bin/node node /usr/bin/nodejs 10` Now if you do a sudo which node you'll see it points to /user/bin/node 4. Install NPM (node package manager) next `sudo apt-get install npm` Clone the Repository 5. Change to your standard projects, folder mine is in /home/sumitkm/MyProjects/github `git clone https://github.com/atom/atom` 6\. Checkout the latest atom release ``cd atom git fetch -p git checkout $(git describe --tags `git rev-list --tags --max-count=1`)`` 7\. Build Atom into a custom folder. I created a /build folder under /home/sumitkm/MyProjects/builds `script/build --build-dir /home/sumitkm/MyProjects/builds/atom` This will take a while as it downloads and installs all the packages required to build Atom and then does the actual build. If all goes well, you should have a success message at the end of the installation. Note: If you have not restarted the terminal/console after installing node and the installation fails, restart the terminal and you SHOULD NOT require a sudo to run the script. If you get a deduping error clear out the ../github/atom/node\_modules folder using rm -rf. 8. Install Atom as `sudo script/grunt install --build-dir /home/sumitkm/MyProjects/builds/atom` You are now all set to use Atom and also with NodeJS should you want to build NodeJS services.

## Looking Back...

I did not expect it to be all sunshine and bunny rabbits when I decided to give Linux a try. But it has not been that bad. The VM on my desktop just works marvellously. The on the metal laptop has a few quirks, that I am sure I can sort out. Linux desktop remains the enthusiast's OS but it has grown well I'll say. And of course the amount of documentation out there is also pretty phenomenal. This experiment shall continue well into my new laptop whenever I get it...
