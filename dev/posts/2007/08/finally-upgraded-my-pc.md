---
author: "Sumit"
title: "Finally Upgraded my PC"
date: "2007-08-04"
categories: 
  - "hardware"
tags: 
  - "computer-hardware"
  - "computer-upgrade"
---

I've wanted to upgrade my PC from the ancient Celeron 700 with about 300Megs of RAM to something better for a while now. So finally when in Kolkata for Nemo's B'Day celebration when my Dad's P4's HDD crashed, I got a chance to revisit my friendly neighbourhood computer parts supplier. I've been assembling my own PCs for about a decade now. In the recent past I had the opportunity to ogle at the Mac Mini running OS X at a friends' place in US. Back in India, one window shopping tour thru an Apple store and the G5 was a great temptation. Still the fact that I make my living working on MS technology stack made the final decision pretty easy.

Before the actually shelling out the bucks did a quick search for motherboard models from ASUS because there were rumours that the Intel Original Boards were being too cranky for comfort. So with a scribbled list of 5-6 m/b names I went shopping for my new 'PC'. Ended up with the following:

1\. Intel core 2 Duo @ 2.0 GHz (800 MHz FSB and 2MB L2 cache)

2\. ASUS P5B MX/WiFi AP Motherboard with onboard Gb/s LAN, Wifi Support, Realtek HD Audio, 6USB Ports, 4 SATA, 1 UDMA IDE and 1 Floppy Drive support, 2 DDR SDRAM slots.

3\. 2 sticks of Transcend 1GB DDR SD running at 667MHz

4\. 250 GB 7200 RPM Seagate SATA HDD

5\. A Samsung DUAL Layer DVD R

6\. Windows Vista Business OEM

7\. Norton Antivirus for Dad's PC

Total bill came to approx 27K INR which is < $700.

Since I had to carry all this back to Pune didn't purchase the cabinet/power-supply needed to house the new PC.

The lack of Cabinet posed a small challenge of testing the whole setup before going back to Pune. Luckily enough my Uncle had recently purchased a new P4 Machine. So off I went to his place.

The new socket was a surprise but the bigger surprise was the CPU it self (look Ma no Pins!!!). Anyways, gingerly placed the CPU and even more tentatively pushed the lever back on. Then went the HUGE CPU cooler fan. RAM was easy. Unplugging the other machine's power-supply and plugging it into my M/B was challenge in itself. Ended up with a plywood plank across the cabinet that supported my MB/HDD and DVD. With this precarious setup, switched on the PC and lo! it worked the first time. Yipppieeeee!!!

In went the Vista DVD and thus started the installation process. Was relatively painless as Vista seemed to have drivers for everything even though the M/B had come with drivers for graphics card and WiFi (beta for Vista). Took about an hour to complete the setup including partitioning the 250GB HDD into 3 roughly similar sized partitions and formating the C:. First step successful. All h/w validated.

Back in Pune, bought a Frontech Cabinet, Supercomp 450 watts power supply (said ATX 2.03 compliant whatever it means) a cheap PS/2 key board (plan to go for a wireless k/b and mouse setup soon) and an extra cabinet fan to prevent the CPU from getting fried too soon. Assembled everything in place and booted up. No issues. Next step connecting to my Linksys wireless router and thru it to the Internet via the broadband modem. Funnily enough the wireless router was in a reset state and had to be reconfigured completely to connect to the net. That done Vista quickly connected to the net. Though the inability to do a ipconfig/release and renew led to some anxious moments. But it detected Internet on its own accord that had worked till about the first 25% of this blog. Somehow had to reset the router to get back to the net now. Thanks to the reset the Orcas beta download got messed and has now restarted.

On fiddling around for a while managed to get to the device manager in Vista which showed three unknown/conflicting devices. So first I put the m/b device driver CD that installed the Graphics Card Drivers and Audio drivers that brought the number of unknown/conflicting devices to 2. A full windows update resulted in one of the unknown drivers getting identified as Atheros AR57007 Wireless Network Adapter. Still it was 'conflicting'. Now I was beginning to get jittery. Went to asus website and downloaded the latest drivers for the WiFi card and installed. Reboot. Voila!!! All devices identified and no longer conflicting. Enabled the wireless device and played around with it to ensure it was working both as Access Point and Base station. As I disabled it, BAM! The dreaded BSOD. Some stupid error saying IRQ\_NOT\_LESS\_OR\_EQUAL and a subsequent memory dump. Nasty, very nasty. Reboot, google google google... Seems it could be bad memory. Dug out MemTest and left it on for the rest of the night. after 600% testing no errors. So no bad RAM. Left it as it is.

It has been a week now and the machine has been running almost 14-16 hours a day. No issues so far except for the drop in internet connection earlier today while typing this blog.

Somewhere in between, enabled the Vista Aero Effects and the desktop now looks impressive with all the glassy/translucent effects. Yes it is reminiscent of the OS X, but I am not complaining. If anything it's a 'better looking' windows. Too used to Firefox now and downloading Firefox is probably the maximum use of IE7 that I did. IE7 is notorious at office with all it's ridiculous popus and content blocking. Our ASP.NET application runs better on Firefox than on IE ;-)...

So far no serious work undertaken on the machine. Will have a better feel of actual performance once I get my hands dirty with Orcas.

Just now dug out the Performance Information Tool and according to it following is the system Performance (with Aero Enabled).

Component Score

Processor Intel(R) Core(TM)2 CPU 4400 @ 2.00GHz 4.9 Memory (RAM) 1.99 GB 4.8 Graphics Intel(R) 946GZ Express Chipset Family 3.8 Gaming graphics 358 MB Total available graphics memory 3.7 Primary hard disk 61GB Free (78GB Total) 5.8

Well, now that I've joined the Vista bandwagon, lets see how it goes. Will keep everybody updated.
