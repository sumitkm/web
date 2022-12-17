---
author: "Sumit"
title: "Trying to upgrade SSD on an old MBP... and failing"
date: "2022-12-16"
categories: 
  - "computers"
tags: 
  - "apple"
  - "osx"
---

I usually take good care of my electronic stuff and they last me a bit. So it is no surprise I am writing this post on my 7 years old Mid 2015 MacBook Pro. This is a Core i7 with 16Gb memory and (unfortunately) 256 Gb SSD. I can go to certain lengths for Apple h/w for their quality but pay 3-5x markup for storage capacity was where I drew the line. 

## The Backstory

Incidentally this MBP model had a battery recall. I've been getting battery recall notices since 2019 or thereabouts. Apple store said 3 weeks downtime when they announced it. I didn't really care for that much downtime and my battery was working fine, so I kept delaying it until recently when I noticed the touchpad woudn't depress which meant the battery had probably swollen up. Dug up the last email from Apple (August 2022) and double checked if I could still request battery replacement, yes, great; Found a Western Computer nearby, dropped off the laptop, less than a week later, I had it back with new battery (keyboard and chassis were replaced too, because it is to dangerous to rip out a swollen, glued up, LiPo battery apparently). Lost my Github and a few other stickers on the palmrest, but I am not complaining. With a new battery this laptop was good for another 5 years technically. Onwards and upwards.

## The SSD Upgrade attempt

So with the laptop good as new, all I needed was to be able to use the laptop like one. Unfortunately thanks to Apple's insistence on hiding everything and not allowing changes to default install folders, I had all but run out of space. 1Tb M.2 SSDs were cheap. After a bit of research I landed on this page [on MacRumors](https://forums.macrumors.com/threads/upgrading-2013-2014-macbook-pro-ssd-to-m-2-nvme.2034976/) Brilliant forum post with loads and loads of details. Looked like a rock solid option, so I bought a Crucial 1TB P2 NVME SSD 
![Crucial 1TB P2 NVME SSD](/images/blog/2022/12/CrucialNVME.jpg)
It looked like a good compromise of speed and energy consumption.
I also bought a so-called Sintech adapter. 
Followed [this video tutorial](https://www.youtube.com/watch?v=KT3IKRYqEJU) to install OS and restore from Backup. All worked flawlessly. I was a happy puppy, but not for long. About 2 weeks in, I started noticing Kernel panics everytime I shut the lid of the laptop and left it for a period of time (like overnight). Most of the time it was the following error

```bash
panic(cpu 0 caller 0xffffff801b3866a2): nvme: "3rd party NVMe controller. Command timeout. Write. fBuiltIn=1 MODEL=CT1000P2SSD8 FW=P2CR048 CSTS=0x1 US[1]=0x0 US[0]=0x1 VID=0xc0a9 DID=0x540a CRITICAL_WARNING=0x0.\n" @IONVMeController.cpp:6090
Panicked task 0xffffff8b6573f670: 167 threads: pid 0: kernel_task
Backtrace (CPU 0), panicked thread: 0xffffff99caa1e000, Frame : Return Address
0xffffffffa974ba20 : 0xffffff8018a7de9d 
0xffffffffa974ba70 : 0xffffff8018be0556 
0xffffffffa974bab0 : 0xffffff8018bcf8c3 
0xffffffffa974bb00 : 0xffffff8018a1da70 
0xffffffffa974bb20 : 0xffffff8018a7e26d 
0xffffffffa974bc40 : 0xffffff8018a7da26 
0xffffffffa974bca0 : 0xffffff80193145e3 
0xffffffffa974bd90 : 0xffffff801b3866a2 
0xffffffffa974bda0 : 0xffffff801b3697cb 
0xffffffffa974bdd0 : 0xffffff80192498e5 
0xffffffffa974be40 : 0xffffff80192497e8 
0xffffffffa974be70 : 0xffffff8018ad0f15 
0xffffffffa974bee0 : 0xffffff8018ad1fe2 
0xffffffffa974bfa0 : 0xffffff8018a1d19e 
      Kernel Extensions in backtrace:
         com.apple.iokit.IONVMeFamily(2.1)[DD1246CA-DCEA-310E-A5EF-D93F9E3160E0]@0xffffff801b361000->0xffffff801b38dfff
            dependency: com.apple.driver.AppleMobileFileIntegrity(1.0.5)[6A4C9635-1909-3C7E-A67E-4A1A31F7CA60]@0xffffff801a1b1000->0xffffff801a1d2fff
            dependency: com.apple.iokit.IOPCIFamily(2.9)[F4541C1C-CF87-39BB-B39E-FFF1E15F61CE]@0xffffff801b636000->0xffffff801b662fff
            dependency: com.apple.iokit.IOReportFamily(47)[B345BB34-190D-36D1-89D3-7904BBDBC2E9]@0xffffff801b674000->0xffffff801b676fff
            dependency: com.apple.iokit.IOStorageFamily(2.1)[58C6FBAD-E214-3CCD-A845-FAC6E5F3958C]@0xffffff801b779000->0xffffff801b78ffff

Process name corresponding to current thread (0xffffff99caa1e000): kernel_task

Mac OS version:
21G217

Kernel version:
Darwin Kernel Version 21.6.0: Thu Sep 29 20:12:57 PDT 2022; root:xnu-8020.240.7~1/RELEASE_X86_64
Kernel UUID: 54B44BAE-1625-30CC-80B0-29E4966EFFDC
KernelCache slide: 0x0000000018800000
KernelCache base:  0xffffff8018a00000
Kernel slide:      0x0000000018810000
Kernel text base:  0xffffff8018a10000
__HIB  text base: 0xffffff8018900000
System model name: MacBookPro11,4 (Mac-06F11FD93F0323C5)
System shutdown begun: NO
Panic diags file available: YES (0x0)
Hibernation exit count: 0

System uptime in nanoseconds: 6832382844472
Last Sleep:           absolute           base_tsc          base_nano
  Uptime  : 0x00000636c9c0a5fc
  Sleep   : 0x0000062539b31e1f 0x0000000060138096 0x0000060c7fed6b49
  Wake    : 0x000006254dbdbeb4 0x0000000060c9e17a 0x000006254170b04d
Compressor Info: 0% of compressed pages limit (OK) and 0% of segments limit (OK) with 1 swapfiles and OK swap space
Zone info:
  Zone map: 0xffffff8030fbb000 - 0xffffffa030fbb000
  . PGZ   : 0xffffff8030fbb000 - 0xffffff8032fbc000
  . VM    : 0xffffff8032fbc000 - 0xffffff84ff7bb000
  . RO    : 0xffffff84ff7bb000 - 0xffffff8698fbb000
  . GEN0  : 0xffffff8698fbb000 - 0xffffff8b657bb000
  . GEN1  : 0xffffff8b657bb000 - 0xffffff9031fbb000
  . GEN2  : 0xffffff9031fbb000 - 0xffffff94fe7bb000
  . GEN3  : 0xffffff94fe7bb000 - 0xffffff99cafbb000
  . DATA  : 0xffffff99cafbb000 - 0xffffffa030fbb000
  Metadata: 0xffffffffb9fee000 - 0xffffffffd9fee000
  Bitmaps : 0xffffffffd9fee000 - 0xffffffffdffee000

last started kext at 36530783870: >driverkit.serial	6.0.0 (addr 0xffffff7fb1cb5000, size 28672)
loaded kexts:
>AudioAUUC	1.70
>!APlatformEnabler	2.7.0d0
>AGPM	129
>X86PlatformShim	1.0.0
@filesystems.autofs	3.0
>!AUpstreamUserClient	3.6.9
>!AHDAHardwareConfigDriver	340.2
>!AHDA	340.2
>eficheck	1
>!ALPC	3.1
>!AGraphicsDevicePolicy	6.5.7
@AGDCPluginDisplayMetrics	6.5.7
>pmtelemetry	1
|IOUserEthernet	1.0.1
>usb.!UUserHCI	1
>AGDCBacklightControl	6.5.7
>!AHV	1
>!ADiskImages2	126.141.2
>!ABacklight	180.8
>!A!IHD5000Graphics	18.0.8
>!ACameraInterface	7.9.1
>!AMCCSControl	1.16
>ACPI_SMC_PlatformPlugin	1.0.0
>!AFIVRDriver	4.1.0
>!AMuxControl	6.5.7
>!ASMCLMU	212
>!A!IFramebufferAzul	18.0.8
>!A!ISlowAdaptiveClocking	4.0.0
>!AThunderboltIP	4.0.3
|SCSITaskUserClient	456.140.3
>!ATopCaseHIDEventDriver	5450.8
>!UTopCaseDriver	5450.8
>!UCardReader	533.120.2
>AirPort.BrcmNIC	1400.1.1
>!AFileSystemDriver	3.0.1
@filesystems.tmpfs	1
@filesystems.lifs	1
@filesystems.apfs	1934.141.2
@filesystems.hfs.kext	583.100.10
@BootCache	40
@!AFSCompression.!AFSCompressionTypeZlib	1.0.0
@!AFSCompression.!AFSCompressionTypeDataless	1.0.0d1
@private.KextAudit	1.0
>!ARTC	2.0.1
>!ASmartBatteryManager	161.0.0
>!AACPIButtons	6.1
>!AHPET	1.8
>!ASMBIOS	2.1
>!AACPIEC	6.1
>!AAPIC	1.7
@!ASystemPolicy	2.0.0
@nke.applicationfirewall	402
|IOKitRegistryCompatibility	1
|EndpointSecurity	1
@Dont_Steal_Mac_OS_X	7.0.0
@kec.!AEncryptedArchive	1
>driverkit.serial	6.0.0
|IOSerial!F	11
@kext.triggers	1.0
>DspFuncLib	340.2
@kext.OSvKernDSPLib	529
>!UAudio	416.2
>!AAudioClockLibs	140.1
>!ASMBusPCI	1.0.14d1
>!AHDA!C	340.2
|IOHDA!F	340.2
|IOAudio!F	340.2
@vecLib.kext	1.2.0
|IO!BSerialManager	9.0.0
|IO!BPacketLogger	9.0.0
|IO!BHost!CUSBTransport	9.0.0
|IO!BHost!CUARTTransport	9.0.0
|IO!BHost!CTransport	9.0.0
>IO!BHost!CPCIeTransport	9.0.0
|IOAVB!F	1040.6
@plugin.IOgPTPPlugin	1040.3
|IOEthernetAVB!C	1.1.0
|CSR!BHost!CUSBTransport	9.0.0
|Broadcom!BHost!CUSBTransport	9.0.0
|Broadcom!B20703USBTransport	9.0.0
>!AIPAppender	1.0
>!ABacklightExpert	1.1.0
|IONDRVSupport	597
>!ASMBus!C	1.0.18d1
>IOPlatformPluginLegacy	1.0.0
>X86PlatformPlugin	1.0.0
>IOPlatformPlugin!F	6.0.0d8
>!AGraphicsControl	6.5.7
|IOAccelerator!F2	462.8
@!AGPUWrangler	6.5.7
@!AGraphicsDeviceControl	6.5.7
|IOGraphics!F	597
|IOSlowAdaptiveClocking!F	1.0.0
>!AThunderboltEDMSink	5.0.3
>!AThunderboltDPOutAdapter	8.5.1
>!AActuatorDriver	5460.1
>!AHS!BDriver	5450.8
>IO!BHIDDriver	9.0.0
>!AMultitouchDriver	5460.1
>!AInputDeviceSupport	5460.1
>!AHIDKeyboard	228.2
>usb.IOUSBHostHIDDevice	1.2
>usb.cdc	5.0.0
>usb.networking	5.0.0
>usb.!UHostCompositeDevice	1.2
>!AThunderboltDPInAdapter	8.5.1
>!AThunderboltDPAdapter!F	8.5.1
>!AThunderboltPCIDownAdapter	4.1.1
>!AXsanScheme	3
>!AThunderboltNHI	7.2.81
|IOThunderbolt!F	9.3.3
|IO80211!FLegacy	1200.12.2b1
|IOSkywalk!F	1.0
>mDNSOffloadUserClient	1.0.1b8
>corecapture	1.0.4
|IONVMe!F	2.1.0
>!A!ILpssGspi	3.0.60
>usb.!UXHCIPCI	1.2
>usb.!UXHCI	1.2
>!ABSDKextStarter	3
|IOSurface	302.14
@filesystems.hfs.encodings.kext	1
>usb.!UHostPacketFilter	1.0
|IOUSB!F	900.4.2
>!AEFINVRAM	2.1
>!AEFIRuntime	2.1
|IOSMBus!F	1.1
|IOHID!F	2.0.0
|IOTimeSync!F	1040.3
|IONetworking!F	3.4
>DiskImages	493.0.0
|IO!B!F	9.0.0
|IOReport!F	47
$quarantine	4
$sandbox	300.0
@kext.!AMatch	1.0.0d1
|CoreAnalytics!F	1
>!ASSE	1.0
>!AKeyStore	2
>!UTDM	533.120.2
|IOUSBMass!SDriver	210.120.3
|IOSCSIBlockCommandsDevice	456.140.3
|IO!S!F	2.1
|IOSCSIArchitectureModel!F	456.140.3
>!AMobileFileIntegrity	1.0.5
$!AImage4	4.2.0
@kext.CoreTrust	1
>!AFDEKeyStore	28.30
>!AEffaceable!S	1.0
>!ACredentialManager	1.0
>KernelRelayHost	1
|IOUSBHost!F	1.2
>!UHostMergeProperties	1.2
>usb.!UCommon	1.0
>!ABusPower!C	1.0
>!ASEPManager	1.0.1
>IOSlaveProcessor	1
>!AACPIPlatform	6.1
>!ASMC	3.1.9
|IOPCI!F	2.9
|IOACPI!F	1.4
>watchdog	1
@kec.pthread	1
@kec.Libm	1
@kec.corecrypto	12.0

```

Quite obvious OSX wasn't playing ball with the NVME drive.

Went back to the forum page, tried everything listed, reseating, disabling power savings even changing the adapter, but nothing worked. I even looked for SSD firware upgrade, but my firmware version is far ahead of what Micron offers on its site. They offer 33 something, while mine show 40 something. So could be the SSD isn't quite compatible with OSX anymore.

Worried that I was ruining the SSD (some forums said, continuing with the Kernel panic would eventually corrupt the entire SSD), I broke down and reverted to the old Apple SSD. For a very long time I had used a 256Gb Samsung USB stick. It is super tiny and was absolutely unobtrusive. But an USB stick is a USB stick, you always have the 'threat of failing' hanging over your head!

So in the end I bought a case for NVME M.2 drive and started using it as a USB drive. Hoping it lasts longer than the USB stick, though I can't quite wrap my head around, why that would be the case.

## A possible way forward

Why do I need more storage:

1. Photos
2. Music
3. Hobby projects

I can move Hobby projects to the external drive no issues. But the thing about OSX is you can't beat the system, so you have to join the system. So everything goes in folders that the app decides. iCloud Drive has it's own location and you can't really change that easily. iPhotos, ditto, Music same you get the gist. 

I did a bit of research and so far I've found you can move [System Photo Library in Photos](https://support.apple.com/en-us/HT204414). 
You can also move the [Music App folder](https://support.apple.com/en-gb/guide/music/mus69248042d/1.2/mac/12.0).
Still looking how I can move iCloud Drive folder elsewhere.

I haven't tried any of this yet, because I also found I could boot from the USB drive, so I am a little conflicted if I want the laptop to boot of the USB connected drive. 

Eitherway, that was my attempt at upgrading my 7 year old laptop. Hopefully it saves you some hair pulling.