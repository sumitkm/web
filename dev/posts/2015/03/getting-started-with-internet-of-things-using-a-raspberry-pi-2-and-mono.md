---
title: "Getting started with Internet of things using a Raspberry Pi 2 and Mono"
date: "2015-03-22"
categories: 
  - "iot"
  - "raspberrypi"
tags: 
  - "gpio"
  - "raspberry-pi"
---

Some of you may have spotted my previous experiments with the $35 wonder computer that's the Raspberry Pi. I have since then added two more Raspberry Pies to my collection. One goes into the amazeballs Diddyborg (by @Pi\_Borg) and the other one is a the latest and greatest Raspberry Pi 2 bought on the day of launch in early February.

The Diddyborg is nice kit created by PiBorg.org. It showcases their motor controller which can control 6-8 motors at a time per controller. It also has the 'batt bot' board included which works towards prolonging the battery life for the Diddborg. It comes with a bunch of sample programs like ball follow that uses optical image recognition via the Pi Camera module. It was a nice fun project that I did with junior over Christmas. I also ended up doing a small keyboard driver using python for it. The current code for it is [up here](https://github.com/sumitkm/diddyberry/tree/master/kbcontroller "Github - Diddyberry (Experiments with my Diddyborg)") (not the best Python ever written, you have been warned). There are lots of experiments planned with it, but that's for another day.

I have been sitting on the sidelines of the Internet of Things (IoT) buzz for a while now and waiting for the 'right moment'. Apparently the trigger was launch of the rather capable Raspberry Pi 2 early in February this year. With the bump in spec to a Quad Core 900MHz processor with 1 Gig of RAM, the Raspi 2 is about as capable as mid-market contemporary smartphone. At 25GBP it's a steal!!! Along with the Pi I bought a microcontroller controlled 8 relay board. Idea was to toggle lightbulbs on/off from my phone ![Smile](images/wlemoticon-smile.png). There are ready made kits, ready made bulbs already in the market. So it's not ground breaking, but hey, where's the fun in that right!

Anyway, I missed the first lot of Pi deliveries but manage to squeak into the second lot. The microcontroller board arrived quickly enough but the female-female jumper connectors took forever to arrive from Hong Kong. Here's the entire kit:

1\. Raspberry Pi 2 + Power Supply + 16Gig SD card (went big assuming Win IoT would be a massive hog). 2. 5V 10A, 8 Relay microcontroller board by Anoder. The relays are not opto-coupler (aka solid state relays) and are ON when low meaning the connection is ON without any input. You have to provide an input to turn it off. This is good in a way that you can expect your lights to remain on (and in control of the mains switch) if your Pi crashes. However it also means while programming it, you have to send in a 1 to turn it off and 0 to turn it on. Kinda reversed! 3. 40 pin Female-Female jumper cables. 4. Optionally I bought a breadboard and a bunch of breadboard connection wires.

## Wiring things up

After untold warnings on the internet about not working on mains power I decided to heed to people's warning and play with my LED Christmas lights that already had a 220 - 12V step down. (NOTE: I am not a certified electrical engineer in UK, but I DO know my way around electrical boards, supplies and wiring and have had enough 'shocking' experiences as a kid to not treat 240V mains supply lightly). So this blog will not show you stuff beyond driving the relay. What you connect to the other side of the relay is up to you. I used a Christmas light that works off a 5V DC supply provided by a built in control unit.

To run this code you don't need anything on the other end of the relays. You can hear the Relays click quite distinctly and there is an indicator LED that will also give you ample hint that the relays are working.

### Pin Outs

I connected two of the 8 relays to GPIO 17 and GPIO 22. So the connections were like this

[![GPIOtoRelay](images/gpiotorelay_thumb.png "GPIOtoRelay")](/images/blog/2015/03/images/blog/gpiotorelay.png)

The board on the left is a not-to-scale representation of the Raspberry Pi 2 as seen from the CPU side. The GPIO ports take up more space on my diagram than in the actual board, but you get the point.

I have only labeled some of the pins to keep the diagram clean (actually to get it done quickly enough). Here is a [complete pin out](http://pi.gadgetoid.com/pinout "Raspberry Pi Pin out") if you need one handy!

Like the Pi board, the Relay board diagram is representative and not to scale too. The blue boxes are the relays and the Red diode symbols represent the LEDs on board.

### Connections

IO Pin 2 is what is powering the relay controller. So it's connected to the VCC pin of the Relay board (Brown wire on my connector strip). IO Pin 6 ground is connected to the ground (first pin) of relay board (Green wire on my connector strip) IO Pin 11 represents GPIO 17 (blame Broadwell the CPU makers for the weirdness in numbering schemes). A 0 or 1 to GPIO 17 will drive the first relay hence it's connected to **In 1** on the relay board using the red wire from the connector strip. IO Pin 15 represent GPIO 22. I've connected it to **In 2** on the relay board using the blue wire from the connector strip.

That covers the wiring between the Pi and the Relay board.

## Switching Relays using Python

To test the controller board out, I first tried a sample Python program. The source is here. As you can see it's pretty rudimentary but it did what it was asked to do. Switch the lights off for 20 seconds.

But I wanted more. I wanted to direct the GPIO ports over the web. I tried reading up on making web services in Python and realized there wasn't a quick way out. That's when I came across Jan Tielens' excellent series on getting started with .NET on Raspberry Pi.

[This article](http://j.tlns.be/2015/02/getting-started-with-the-raspberry-pi-2-for-net-developers/ "Getting started with the Raspberry Pi 2, for .NET developers") by Jan will get the Pi Setup with Mono + MonoDevelop. Jan starts with a barebones Pi and walks you all the way up to the Mono Setup. If you just want to setup Mono here is the gist:

1.Update Wheezy package list to the latest

\[sourcecode language="actionscript3"\] sudo apt-get update \[/sourcecode\]

2\. Upgrade Wheezy to latest and greatest

\[sourcecode language="bash"\] sudo apt-get upgrade \[/sourcecode\]

3\. Retrieve and install key for the mono GPG key

\[sourcecode language="bash" padlinenumbers="true"\] sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \[/sourcecode\]

4\. Next add repository reference to apt-get. This is where the mono-repositories are (two repository references).

\[sourcecode language="bash"\] echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list

echo "deb http://download.mono-project.com/repo/debian wheezy-apache24-compat main" | sudo tee -a /etc/apt/sources.list.d/mono-xamarin.list \[/sourcecode\]

5\. Repeat step 1 and 2 to make sure all dependencies are in place.

6\. Install Mono (finally)!!!

\[sourcecode language="bash"\] sudo apt-get install mono-complete \[/sourcecode\]

7\. Install MonoDevelop (for on Pi development)!

\[sourcecode language="bash"\] sudo apt-get install monodevelop \[/sourcecode\]

A lot of people develop on Visual Studio and deploy on the Pi. But MonoDevelop is a very capable IDE and I wanted to develop on device. So I opted to use MonoDevelop for my Pi development.

Once I had C# running on Pi, the world was my oyster. I realized how brave a path Miguel Icaza had blazed when he started the Mono project. I am no OSS fanatic, but I am no shill either. Heartfelt thanks to the Mono Team for sticking around against lots and lots of odds. Yes, now I believe you guys love C# more than Microsoft itself does!

## Talking to GPIO pins using C#

Once I had C# going, I followed some more of Jan's tutorials to see how you could communicate with GPIO pins. Turns out the GPIO port is registered as a folder (like most devices on Linux), and all I had to do was write appropriate 'text' to appropriate files in assorted folder. Since this all sounded very easy I assumed someone had already done the hard work. Indeed there are two nice libraries on Github. However when I tried to use RaspberryGPIOManager I found it was locking itself up (on the Raspberry Pi 2). So my friend Raj and I got busy following Jan's tutorial and write the code ourselves. Sure enough, Raj had the code going in about 45 minutes and were were able to talk to one of the GPIO ports and do the same thing the Python program was doing.

Next day I sat down and wrote up a rudimentary library in line with RaspberryGPIOManager and now it's a neat reusable component.

## Show me the code

Okay, enough rambling, time to see some code.

I started with a simple Console application on Mono and split up the reusable component into a separate class library. So essentially I have two projects

1\. My IoT library (PiOfThings) that for now has the GPIO interaction library (GPIOManager) and

2\. Sample code (GpioCs).

### GPIO Manager

The GPIO Manager project has two files GPIOManager.cs which is the actual driver and GPIOPinReferences.cs a bunch of helpers and enumerations.

#### GPIOPinReferences.cs

This file has two static classes and two enums. The GPIOPinState enum does what it says, encapsulates the Pin statuses which is essentially 0 or 1 with 3 indicating error/unknown condition.

\[sourcecode language="csharp" padlinenumbers="true"\] public enum GPIOPinState { Low = 0, High = 1, Unknown = 3 } \[/sourcecode\]

The second enum called GPIOId maps directly to the pin numbers on the Raspberry Pi 2 (or B+) I/O port. GPIOUnknown is assigned the value -1 for any non GPIO pins.

\[sourcecode language="csharp"\] public enum GPIOId { GPIOUnknown = -1, GPIO02 = 2, GPIO03 = 3, GPIO04 = 4, GPIO07 = 7, GPIO08 = 8, GPIO09 = 9, GPIO10 = 10, GPIO11 = 11, GPIO14 = 14, GPIO15 = 15, GPIO17 = 17, GPIO18 = 18, GPIO22 = 22, GPIO23 = 23, GPIO24 = 24, GPIO25 = 25, GPIO27 = 27 } \[/sourcecode\]

Next we have a helper class that maintains two dictionaries of pin number-to-port and port-to-pin number.

\[sourcecode language="csharp"\] public static class GPIOPinMapping { private static Dictionary&amp;lt;GPIOId, int&amp;gt; GPIOToPin = new Dictionary&amp;lt;GPIOId, int&amp;gt; { { GPIOId.GPIO02, 3 }, { GPIOId.GPIO03, 5 }, { GPIOId.GPIO04, 4 }, { GPIOId.GPIO07, 26 }, { GPIOId.GPIO08, 24 }, { GPIOId.GPIO09, 21 }, { GPIOId.GPIO10, 19 }, { GPIOId.GPIO11, 23 }, { GPIOId.GPIO14, 8 }, { GPIOId.GPIO15, 10 }, { GPIOId.GPIO17, 11 }, { GPIOId.GPIO18, 12 }, { GPIOId.GPIO22, 15 }, { GPIOId.GPIO23, 16 }, { GPIOId.GPIO24, 18 }, { GPIOId.GPIO25, 22 }, { GPIOId.GPIO27, 13 } };

private static readonly Dictionary&amp;lt;int, GPIOId&amp;gt; PinToGPIO = new Dictionary&amp;lt;int, GPIOId&amp;gt; { { 1, GPIOId.GPIOUnknown }, { 2, GPIOId.GPIOUnknown }, { 3, GPIOId.GPIO02 }, { 4, GPIOId.GPIO04 }, { 5, GPIOId.GPIO03 }, { 6, GPIOId.GPIOUnknown }, { 7, GPIOId.GPIOUnknown }, { 8, GPIOId.GPIO14 }, { 9, GPIOId.GPIOUnknown }, { 10, GPIOId.GPIO15 }, { 11, GPIOId.GPIO17 }, { 12, GPIOId.GPIO18 }, { 13, GPIOId.GPIO27 }, { 14, GPIOId.GPIOUnknown }, { 15, GPIOId.GPIO22 }, { 16, GPIOId.GPIO23 }, { 17, GPIOId.GPIOUnknown }, { 18, GPIOId.GPIO24 }, { 19, GPIOId.GPIO10 }, { 20, GPIOId.GPIOUnknown }, { 21, GPIOId.GPIO09 }, { 22, GPIOId.GPIO25 }, { 23, GPIOId.GPIO11 }, { 24, GPIOId.GPIO08 }, { 25, GPIOId.GPIOUnknown }, { 26, GPIOId.GPIOUnknown }, { 27, GPIOId.GPIOUnknown }, { 28, GPIOId.GPIOUnknown }, { 29, GPIOId.GPIOUnknown }, { 30, GPIOId.GPIOUnknown }, { 31, GPIOId.GPIOUnknown }, { 32, GPIOId.GPIOUnknown }, { 33, GPIOId.GPIOUnknown }, { 34, GPIOId.GPIOUnknown }, { 35, GPIOId.GPIOUnknown }, { 36, GPIOId.GPIOUnknown }, { 37, GPIOId.GPIOUnknown }, { 38, GPIOId.GPIOUnknown }, { 39, GPIOId.GPIOUnknown }, { 40, GPIOId.GPIOUnknown }, };

\[/sourcecode\]

Two static methods help you get the appropriate values out of the dictionaries depending on what you are looking for (pin number or GPIO id).

\[sourcecode language="csharp" firstline="67"\] public static int GetPinNumber (GPIOId gpioNumber) { return GPIOToPin \[gpioNumber\]; } public static GPIOId GetGPIOId(int pin) { if (pin &amp;gt; 0 &amp;amp;&amp;amp; pin &amp;lt;= 40) { return PinToGPIO \[pin\]; } else { throw new ArgumentOutOfRangeException (&amp;quot;pin&amp;quot;, string.Format (&amp;quot;Invalid pin {0}. Please enter value between 1 and 40 (both inclusive).&amp;quot;, pin)); } } } \[/sourcecode\]

### The Driver (GPIOManager.cs)

#### Overview of communication mechanism

A GPIO pin like any digital connection can represent either 0 or 1. 'Talking', 'connecting', 'sending signal' or 'communicating' to a GPIO port simply means you are either reading values (0 or 1) or writing values (0 or 1). Since the Linux OS represents the I/O ports as streams you can using any File System based APIs and a direct your output to specific folders to write to appropriate files.

For GPIO communication on the Pi, the specific folder is as follows

/sys/class/gpio/gpio{pin id}/value

Here {pin id} is the GPIO pin number as specified in the GPIOId enum above

This destination can be used to write "0" or "1" for sending low or high signals to the pin.

To read, you use the same destination but instead of Writing to it, you read from it using FileSystem.

Before you can communicate with a particular pin you need to make sure no one else is communicating with it, so you should try to 'Reserve' the pin and then set "Direction" of communication. Again all this can be done by writing appropriate values to the ports via the file system.

So the API that we are writing as the following calls:

1\. Select (Reserve) a pin

2\. Write to pin

3\. Read from pin

4\. Release pin

#### The actual code

I'll break up the actual code into the above mentioned calls. You can refer to the entire thing together on Github.

The GPIOManager has a readonly GPIO\_ROOT\_DIR folder that can be passed in the constructor if you want to mock the PI and run the manager when the actual GPIO pins are not available.

The Manager has an internal list of Pins that have been selected and hence are busy. Note the Manager is not a singleton so this list may not be the single source of truth on the Pi.

You call the SelectPin method and provide the GPIOId identifying the pin that needs to be selected.

If successful, the CurrentPin property on GPIOManager is set to the pin you requested for, else it throws an exception.

The private call to ReservePin function is what actually selects the Pin. All it does is writes to the 'export' stream, value of the Pin that's selected.

Once you have Selected a pin you can write to the pin using the WriteToPin call.

\[sourcecode language="csharp"\] public bool WriteToPin (GPIOPinState state) { try { File.WriteAllText (String.Format (&amp;quot;{0}gpio{1}/direction&amp;quot;, GPIO\_ROOT\_DIR, CurrentPin.ToString (&amp;quot;D&amp;quot;)), GPIOPinDirection.Out); File.WriteAllText (String.Format (&amp;quot;{0}gpio{1}/value&amp;quot;, GPIO\_ROOT\_DIR, CurrentPin.ToString (&amp;quot;D&amp;quot;)), state.ToString (&amp;quot;D&amp;quot;)); return true; } catch (Exception ex) { Console.WriteLine (&amp;quot;Failed to WriteToPin: &amp;quot; + CurrentPin.ToString (&amp;quot;D&amp;quot;) + &amp;quot; &amp;quot; + ex.Message + &amp;quot;\\n&amp;quot; + ex.StackTrace); } return false; } \[/sourcecode\]

As you can see the WriteToPin call is essentially creating a File handle using the Fire.WriteAllText helper and first setting the Direction in the 'direction' stream.

Next writing the actual value  (0 or 1) to the 'value/\[pin\]' stream.

Similarly if you are reading from the GPIOPin, after you have selected the pin you use the ReadFromPin API.

\[sourcecode language="csharp"\] public GPIOPinState ReadFromPin (GPIOId pin) { GPIOPinState currentState = GPIOPinState.Unknown; try { string state = File.ReadAllText (String.Format (&amp;quot;{0}gpio{1}/value&amp;quot;, GPIO\_ROOT\_DIR, pin.ToString (&amp;quot;D&amp;quot;))); currentState = (state == &amp;quot;1&amp;quot; ? GPIOPinState.High : GPIOPinState.Low); } catch (Exception ex) { Console.WriteLine (&amp;quot;Failed to ReadFromPin: &amp;quot; + pin.ToString (&amp;quot;D&amp;quot;) + &amp;quot; &amp;quot; + ex.Message + &amp;quot;\\n&amp;quot; + ex.StackTrace); } return currentState; } \[/sourcecode\]

ReadFromPin API again uses the File handle at the 'value/\[pin\]' stream and reads the value, that is either "0" or "1" and returns the appropriate GPIOPinState value.

Once Read/Write operation is done you have to Release the pin by calling the ReleasePin API, that needs the GPIOId of the pin you want to release. There is a helper method that Releases the CurrentPin selected.

\[sourcecode language="csharp"\] public bool ReleasePin (GPIOId pin) { try { File.WriteAllText (GPIO\_ROOT\_DIR + &amp;quot;unexport&amp;quot;, pin.ToString (&amp;quot;D&amp;quot;)); \_busyPins \[pin\] = false; CurrentPin = GPIOId.GPIOUnknown; return true; } catch (Exception ex) { Console.WriteLine (&amp;quot;Failed to ReleasePin: &amp;quot; + pin.ToString (&amp;quot;D&amp;quot;) + &amp;quot; &amp;quot; + ex.Message + &amp;quot;\\n&amp;quot; + ex.StackTrace); } return false; } public bool ReleasePin () { return ReleasePin (CurrentPin); } \[/sourcecode\]

That completes our GPIOManager API. Lets write a sample to use it.

### A Sample Console Application

I added a simple console project to the mix and wrote the following in the Program.cs' main function.

All it does is sends a Low on GPIO pin 17 and 22 and waits for a 'return' on the console. Once you hit return it cleans up by releasing the pins and exits.

\[sourcecode language="csharp"\] namespace GpioCs { class MainClass { public static void Main (string\[\] args) { try { GPIOManager gpioManager = new GPIOManager(); gpioManager.SelectPin(GPIOId.GPIO17); gpioManager.WriteToPin(GPIOPinState.Low); Console.ReadLine(); GPIOPinState state = gpioManager.ReadFromPin(gpioManager.CurrentPin); Console.WriteLine(&amp;quot;Current Pin 17: &amp;quot; + state);

gpioManager.SelectPin(GPIOId.GPIO22); gpioManager.WriteToPin(GPIOPinState.Low); Console.ReadLine(); GPIOPinState state22 = gpioManager.ReadFromPin(gpioManager.CurrentPin); Console.WriteLine(&amp;quot;Current Pin 22: &amp;quot; + state22);

Console.WriteLine(&amp;quot;Press enter to close!&amp;quot;); Console.ReadLine(); gpioManager.ReleasePin(GPIOId.GPIO17); gpioManager.ReleasePin(GPIOId.GPIO22); Console.WriteLine (&amp;quot;Completed without errors&amp;quot;); } catch (Exception ex) { Console.WriteLine(ex); } } } } \[/sourcecode\]

In my case this flips on the first and second relays. So even if you don't have anything connected to the relays you'll hear them 'click' on and off. The LED indicator on the board for each relay will glow as well.

## Conclusion

With this simple code we have opened up a plethora of opportunities for us. Next step would be to bundle the code inside a service and then respond to web requests. My idea is to make the service a SignalR client that will connect to a CnC server on the Web/Cloud. The CnC server will have a Web interface allowing you to switch each relay on or off. Now once you connect the relays to appropriate electrical devices you are good to control those devices from the web.

[Code on Github](https://github.com/sumitkm/IoTLightbulb/tree/Part1 "IoTLightbulb project").
