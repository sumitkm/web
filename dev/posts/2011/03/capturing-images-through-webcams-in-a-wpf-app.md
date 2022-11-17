---
title: "Capturing images through webcams in a WPF app"
date: "2011-03-13"
categories: 
  - "net"
tags: 
  - "image"
  - "image-capture"
  - "imagingdevice"
  - "webcam"
  - "wpf"
---

## The Need

I was setting up my Dad’s account on my laptop today when Win 7 provided me with the inane out-of-the box images it cans by default. I immediately thought of capturing an image using the webcam but realized unlike OSX, Win 7 doesn’t have such a utility available. Most laptop manufacturers provide horrendously bloated software to do such type of things but my ‘bootcamped’ Windows 7 setup doesn’t have any of that.

## The Options

The nerd that I am, I wanted to ‘roll my own’ immediately. I had seen Silverlight now has webcam support built-in so if Silverlight can do it you can do the same in WPF right? Dead Wrong! Silverlight runtime uses System.Windows.dll from the Silverlight SDK whereas WPF uses System.Windows from the .NET SDK. Unfortunately the .NET SDK doesn’t have direct support for webcams built in, you’ve to work on it. So I googled it up (with Bing, no jokes, ever since I started using IE9 beta I’ve let Bing remain the default search engine). The options presented were:

1\. WPF Mediakit from CodePlex : [http://wpfmediakit.codeplex.com/](http://wpfmediakit.codeplex.com/ "http://wpfmediakit.codeplex.com/") First glance gave the impression it was too heavy for my needs

2\. Jon Preece’s blog: [http://www.jpreece.com/wpf/webcam-image-capture/](http://www.jpreece.com/wpf/webcam-image-capture/ "http://www.jpreece.com/wpf/webcam-image-capture/") Seemed just right. A little investigation on what ImagingDevice.dll actually does convinced me to go for it using Jon’s code.

3\. Scott Hanselman’s Channel 9 article: [http://channel9.msdn.com/coding4fun/articles/Look-at-me-Windows-Image-Acquisition](http://channel9.msdn.com/coding4fun/articles/Look-at-me-Windows-Image-Acquisition "http://channel9.msdn.com/coding4fun/articles/Look-at-me-Windows-Image-Acquisition") Actually I found this article after I was done manipulating Jon’s code and coming up with the solution below. It also uses Interops so it’s not a pure .NET solution either.

## The Solution – Windows Picture Booth (pre alpha)

Now when I say solution. I mean, the path I took.

Actually the code is pretty simple. I wrapped Jon’s code in a WPF User Control (WebcamCapture.xaml) and added three methods to Start/Stop and Capture current frame.

The WebcamCapture control is hosted on a WPF Form (MainWindow) that has the following control

Button : Start Camera – Does what it says, calls the StartCamera method in the WebcamCapture control.

Button: Stop Camera – Calls the StopCamera method in WebcamCapture control and stops the camera. More like pauses it, because I’ve not cleaned up the last image captured.

Button: Capture Image – Calls the GrabImage method in the WebcamCapture control and shows it adjacent to the web-cam window.

WebcamCapture Control: Shows the feed coming through the web-cam.

Image Control: Shows the last captured image.

TODO: As mentioned above, this is a pre-alpha and right now I am too sleepy to add much else to it. It doesn’t have too much error handling either so expect it to crash an burn on slightest pretext.

But I really want to make this into the OSX equivalent of PictureBooth.

So keep an eye out for the updates.

You can download the entire code from [here](https://1drv.ms/u/s!AjM_-YH7p_afxFe-eH25x9zo_OA_ "Hosted by skydrive")

## Licensing

The code is being made available under GPL. I am still investigating ImagingDevice.dll licensing. I might have to remove it from the download package in future if it infringes someone else’s copyright. From what I’ve read, it’s supposed to come with Windows.
