---
author: "Sumit"
title: "Solaris on x86, Fingerprint Protected CDs and another variation of Muphy's Law."
date: "2007-01-16"
tags: 
  - "cd"
  - "murphys-law"
---

The day started as usual, me and my roomie making it to office at about 9 in the morning. First agenda of the day was to try and setup Solaris 10 on an x86 machine. Before that I had to face my boss to whom I sheepishly admitted that I had run out of permutations and combinations for installing the ([!@#\*&T](mailto:!@#*&T)) Sun Portal Server 7 on various flavours of Linux and that I was going to try installating it on Solaris.

For that I had to get Solaris installed first.

I've grown up on MS technologies and I swear by (at?) them. I stay away from the \*nix world as much as possible. Gave up on terminal and command line interfaces with the advent of Win95. Linux was fine... Solaris was getting too deep... With crossed fingers inserted CD1 and rebooted the machine. Upon restart I see a (unfamiliar) bootmenu.

Okay so far so good. Selected the first option... after a few cryptic outputs the window went blank and then .................... seemed like the installer was swearing at me! After a while it gave up with 'not enough memory' error. 'Not enough memory'... umm... interesting... a quad processor machine with 4 Gig RAM and it still runs out of memory? Not good. I need a Pro for this. Went back to boss. By now he's on the verge of giving up on me... Hold on... couple of phone calls later he's like 'get the software up on solaris STOP'. Hmm... that didn't help, I rope in a friend who had earlier cheekily refused to acknowledge that he knew anything to do with Solaris installation. Showed him the error... he's like okay I'll check gimmie 5 minutes... okay... I go and lookup the Hardware Compatibility List for Solaris. My machine misses the 'cut' by 20. I mean upto model 670 is on the list. Mine is 690! Sigh! My idea of \*nixes is primitive systems with very little or no support for new hardware. So my heart is already sinking. Thankfully I find a tool that's supposed to tell me if Solaris is going to run on my machine. Wow! Download! Cut CD! Run! After a while it says it can't find drivers for the sound card and SATA controllers. Okay, not very bad. Sound cards can be damned... SATA controllers... umm... does this machine have SATA or PATA drives? Reboot!!! BIOS Setup!!! Okay... PATA drive. Good so what's wrong with the setup. Reboot again... This time after swearing for a while I get a new Menu asking if I wanted to do Graphical Install, Terminal install etc etc.

Graphical Install WOAH!!! Lets ROLL!!!... about 10 screens later it does a memory dump and aborts.... Now WHAT!!!. Take the CD out. It seems someone wanted to protect the contents of the CD and has given fingerprint protection a whole new meaning. The CD is smeared with fingerprints. Sigh!!! Cut a new CD now... Reboot... After the usual exchange of swear words between me and the installer I see a graphical window... X has started.... WOW!!! After some mandatory steps the status bar starts rolling. Its a tad slower than Linux. After about an hour/hour and half and 5 CDs. Installation is kind of done and it boots up. On logging in I am greeted with an ancient looking GUI desktop. DUH!!! Anyway that was smoother than expected....

Now the actual fun starts...

Lets get the Portal Server Installation on the way... Insert CD... Extract Zip... run Installer... Fizzzzzz... Installer only works with Linux. OUCH!!! Okay I had downloaded all flavours on my laptop... scramble scramble... Hey only the Linux version remains... Oops... I deleted the non linux favours two days back because I needed room for the Oracle downloads...

Arrrrggggghhhhhh... This is happenning for the second time... I guess its a variation of Murphy's law... we could say

**1\. You will need the installers today that you deleted a week back after it was lying around for ages. 2. The need for an installer will ONLY arise a couple of days after you've deleted it or destroyed it.**

Sigh!!! May the downloads begin... (again)
