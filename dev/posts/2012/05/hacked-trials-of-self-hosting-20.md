---
author: "Sumit"
title: "HACKED! Trials of self hosting"
date: "2012-05-01"
tags: 
  - "blogging"
  - "dotnet-host"
  - "hacked"
---

Okay folks, for the last two days (April-May 2012) my domain [www.sumitmaitra.com](http://www.sumitmaitra.com "www.sumitmaitra.com") was hacked and was showing a hackers' page!  As soon as I found out I redirected my domain to this blog instead of the hacked name servers of dotnet-host.

Before I go into lessons learnt if you are still having trouble with the hacked site content, try to log in to your panel at http://panel.dotnet-host.com/ (Update: August 3, 2013 this is not valid anymore, sorry). The forgot password was also working till yesterday.

Delete all the Index.php, Index.chm, Default.asp, Default.html, Index.html and Index.chm files. These were injected by the Hacker. I tried it but before I could see the results my name server change kicked in so I can't vouch it works but most people have been able to restore their sited by deleting these files recursively off every folder.

Multiple lessons learnt

1\. For all my love for [Scott Hanselman](http://www.hanselman.com "Scott Hanselman's Computer Zen"), I should set the default home page of my favorite browser to my site. Sorry [Scott](http://twitter.com/#!/shanselman "Scott's twitter profile"), nothing personal, you are still my fav tech blogger! Basically keep an eye on your site. I dropped the ball for two full days (facepalm).

2\. When a hosting provider is giving a deal that's too good to be true, it might just be so! I think I was paying $4 per month. It was an awesome deal and I paid for the whole year in advance! Doesn't look like my provider will last till the end of the year! Next time on, I am trying out a provider for a month before I put more money into them. There were some feelers I got about the amateurish-ness of www.dotnet-host.com but hey it was a suggested site from [www.asp.net](http://www.asp.net "www.asp.net") so I just went with it. I think dotnet-host cancelled monthly subscriptions but I don't think anyone heard of reversal of yearly subscriptions pro-rated!

3\. Things to look out for

\- Are they sending you passwords in plain text?

I cringed when they sent me the password in plain-text via email, but by then I had paid them for the year, so thought heck go with it. Didn't work out well.

\- Do they have a good admin console?

Their admin console was very amateurish, functional but amateurish. GoDaddy.com on the other hand is a over done pile to junk! Need something in the middle but better be on overdone side than underdone and amateurish.

\- SQL Server access

Their SQL Server access gave me access through Management Studio. Though an awesome feature this is one less layer of security. So be warned. However if you are able to see every other database on the server then your alarm bells should be ringing loud and jangling!!! I had a screen shot of this and I wanted to send it to them but never did! My bad, if you see something like that, raise hell!

4\. If you are doing any serious hosting don't be cheap look around and be safe. I wanted a place to host my .net code and play around. My home page was actually a pass-through to this blog. In other words it was non-critical hosting. I probably lost some SEO points and looks silly to people who visited my URL in the last two days (sorry folks from LinkedIn). My sample apps on a subdomain are still working. Now I gotta find a new provider and move them.

UPDATE:

5\. Having domain registrars different from hosting providers help! Make it a policy if you can.

In case of the dotnet-host fiasco, my domain registrar was different from dotnet-host so I was quickly able to change the name server and forward my domain to this blog through my domain registrar (took about an hour to propagate).

6\. If the hosting provider is so thoroughly hacked rest assured your credit-card info and passwords are NOT safe anymore. Take precautions as required.

That was my first 'getting hacked' experience, not a nice feeling!

Stay alert and stay safe folks!

UPDATE (August 2, 2013):

Removed dead links from above.
