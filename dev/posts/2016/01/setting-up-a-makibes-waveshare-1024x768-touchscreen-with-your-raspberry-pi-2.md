---
title: "Setting up a Makibes (Waveshare) 1024x600 touchscreen with your Raspberry Pi Zero"
date: "2016-01-07"
categories: 
  - "raspberrypi"
tags: 
  - "lcd"
  - "makibes"
  - "pizero"
  - "raspberry-pi"
  - "touchscreen"
  - "waveshare"
coverImage: "wp_20160103_20_58_28_pro.jpg"
---

I have been eyeing a touchscreen to go with one Raspberry Pi from my collection (O\_o), for a while now. The official Raspberry Pi screen is perpetually out of stock and backordered for months. The resellers are charging a hefty markup. Only option left was a third-party screen. After a lot of deliberations I settled down on this screen by WaveShare http://www.waveshare.com/wiki/7inch\_HDMI\_LCD\_%28C%29

My criteria were:

1. Atleast 7 inches (plan to use it as a dashboard at some point)
2. Capacitive touch (Resistive touch isn't as responsive, blame iPhones for ruining us ;-)...)
3. Least number of addon boards to keep things compact
4. Works with stock Raspbian.

From the looks of it, the WaveShare screen checked all the boxes though the last point is still debatable.

It is available from multiple resellers on Amazon. I bought it via In4dealz and fulfilled my Amazon. They were offering a stand and frame for 6 GBP extra. Total cost 46 GBP. Plus, I bought an Anker Astro E1 external battery pack to power the thing. It's 5200 mAh and should be able to power the Pi for a while.

![WP_20160103_15_55_04_Pro](images/images/wp_20160103_15_55_04_pro.jpg)

Here are the unboxing images:

\[gallery ids="1634,1632,1630,1623,1633,1617,1618" type="square"\]

As you can see they come in a neat bundle, well packed but devoid of any instructions what-so-ever. Even for the frame and stand you have to use your 'imagination' to put things together which isn't too bad for the tinkerer in you.

## Setting it up to work with the Raspberry Pi Zero

The sequence I am writing here isn't the same in which I got things working, but things got really simple after I RTFM ;-)

Anyway I will not repeat the mistakes here.

Before you start off make sure you have the latest Raspbian Jessie image setup and running for your Pi Zero.

1. Assuming your Pi Zero is connected to a regular monitor and able to access the internet. Navigate to http://www.waveshare.com/wiki/7inch\_HDMI\_LCD\_%28C%29
2. The Drivers you need are at the bottom of the page (section 5.6) or http://www.waveshare.com/wiki/7inch\_HDMI\_LCD\_%28C%29#Drivers\_for\_Raspberry\_Pi
3. If you are setting up the Pi Zero get the B/B+ drivers for version 4.1.13x. Its about 20 MB download.
4. Once it finishes extract the tar file
    1. sudo tar zxvf _filename_
5. Before you run the executable make sure max\_usb\_current=1 is setup in the /boot/config.txt file.
    1. sudo nano /boot/config.txt
    2. Scroll to the settings and either uncomment the max\_usb\_current line or add it in a new line at the end of the file.
    3. Exit nano (Ctrl +x)
6. Now change into the extracted folder (big massive name starting with RPIB+.).
7. Execute the installer
    1. sudo ./USB\_TOUCH\_CAP\_7.0\_RASPBIAN
8. It takes about 20-30 seconds and reboots automatically.
9. Let it reboot.
10. Shut it down. If your regular monitor freezes on reboot, hot unplug the power
11. Connect the Pi Zero's HDMI out to the LCDs HDMI in using the Pi Zero's adapter and the provided flat HDMI cable.
12. Connect the Pi's Micro USB to the LCDs Micro USB connector via the provided adapter + cable.
13. Power up and you are good to go :-)!
14. If you have an older Raspberry Pi running a version of Raspbian Wheezy, then get the version 3.x drivers. The screen works with them too.
15. You can install a software keyboard called matchbox-keyboard using apt-get, but I have doubts about it because it seems to consume a lot of CPU resources and even after you have closed it doesn't release resource (quickly). I haven't used it a lot though, so I'll give it another go later.

## Assembling the frame/stand

If you bought the additional frame/stand you can assemble it as shown in the slideshow below. The Pi Zero does fit horizontally towards the top of the frame!

\[gallery ids="1624,1616,1619,1620" type="rectangular"\]

And that's it, you are all set.

I powered it using the Anker Astro E1 battery pack. You can do something similar to keep it portable.

I ever get to making this into a portable/carryable 'tablet' I shall post updates here :-).

> EDIT: As suspected the 'drivers' provided by the vendor don't work once you update your Raspberry Pi image. I had found a PHP driver that worked initially, but with the latest update of Raspbian that's broken as well. As of now it is a non-touch screen till I am able to tinker with the PHP driver and get it back online.
> 
> However, to get it working with any stock Raspbian as a screen, all you have to do is add the following lines at the bottom of your config.txt.
> 
> After you have burned the image to an SD card you can simply add the following lines in the config.txt before you put it in the Pi. This way you don't need a separate monitor to get going.
> 
> max\_usb\_current=1
> hdmi\_group=2
> hdmi\_mode=1
> hdmi\_mode=87
> hdmi\_cvt 1024 600 60 6 0 0
