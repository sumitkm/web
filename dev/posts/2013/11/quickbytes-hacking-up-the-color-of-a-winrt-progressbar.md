---
title: "QuickBytes: Hacking up the color of a WinRT ProgressBar"
date: "2013-11-15"
categories: 
  - "net"
  - "modern-windows-apps"
  - "quickbytes"
  - "winrt"
tags: 
  - "windows-8-store-apps"
---

WinRT never ceases to throw a curveball at the you. I was trying to change the default ‘**Violet**’ color of the ProgressBar and ProgressRing to something more ‘in tune’ with my app’s style, but the only ‘violet’ color visible was the Foreground property, but changing it did nothing to change the color of the ‘running dots’.

After ‘[ducking](http://www.duckduckgo.com/)’ around I found a Brush called ProgressBarIndeterminateForegroundThemeBrush. There are two ways to override it.

1\. Create a resource with the same name and assign a different color. You can do it in your App.xaml or in the XAML of the screen you need it updated in as follows:

<Application.Resources> <SolidColorBrush x:Key="ProgressBarIndeterminateForegroundThemeBrush" Color="#FF2EADE8"/> </Application.Resources>

2\. Update the color at runtime in code. I found [this article](http://www.coderox.se/blog/customize-the-color-of-an-indeterminate-progress-bar.aspx) that might come in handy.

Hope this helps someone, it’s a note for me anyway!
