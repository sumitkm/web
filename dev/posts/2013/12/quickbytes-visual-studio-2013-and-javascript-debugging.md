---
author: "Sumit"
title: "QuickBytes: Visual Studio 2013 and JavaScript Debugging"
date: "2013-12-11"
categories: 
  - "asp-net"
  - "mvc"
  - "quickbytes"
  - "visual-studio"
tags: 
  - "debugging"
  - "javascript"
  - "vs2013"
---

Yesterday I found out something new about Visual Studio. Documentation indicates that it has been with us since VS 2012 (maybe earlier) but I encountered it yesterday.

I have a MVC4 project created in VS2010 and some CSHTML files have accrued some JavaScript crud in form of inline <script>…</script>. I usually refactor them out whenever I can but yesterday I was doing something else and wasn’t in a position to refactor the code at that point. So I tried to put in a breakpoint inside one of these script chunks and I couldn’t. So far, I’ve put breakpoints in the runtime page that comes up in Visual Studio’s Solution Explorer and they were are hit when executing in the browser, but yesterday I couldn’t even set a breakpoint.

After a little bit of [ducking](http://www.duckduckgo.com/ "Duck Duck Go") around I found that you could add the following line in the JavaScript to force the debugger where you want to start debugging and then continue with F10/F11 as usual

debugger;

I was initially indignant at Visual Studio that it ‘made’ me do this by default instead of allowing me to set the breakpoint. Looks a step backward, but then I realized that it was likely some setting in my Dev Setup is not right. I haven’t had a chance to investigate what’s not right, and I used the above hack to resolve my current issues. If you know of a way that kicks VS2013 into enabling breakpoints in inline JS code, do let me know.

Inline JS code is BAD and shouldn’t be used, period. But at times when you are prototyping you tend to take liberties, also not everyone in the team has 15 years of experience writing code, so cruft sometimes comes in. If VS is forcing my hand by making me write clean JavaScript code by default, that’s good, but I also want to know the ‘evil’ way to workaround ![Winking smile](images/wlemoticon-winkingsmile.png), Cheers!
