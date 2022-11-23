---
author: "Sumit"
title: "Web Software Devs &ndash; Don&rsquo;t build a Galloping Gertie"
date: "2012-02-13"
tags: 
  - "microsoft"
  - "project-management"
  - "project-management-failure"
  - "security"
---

Woke up today morning (afternoon) to the news that Microsoft Store India’s site had been hacked and it’s plain text user passwords put up for everyone’s benefit!

Now I don’t approve of that action, but I am really appalled and flabbergasted that in 2012 we still have databases that have plain text password stored.

Being a staunch MS loyalist, first thing I did was lookup the default aspnetdb which any n00b developer would use as the starting point. Thankfully even the sample aspnetdb does not store passwords in plain text. That made me even more mad. So the danged n00b who did it, didn’t know/care about the out-of-the-box security framework available. For me this is a bloody failure of the entire s/w development process, the developer, the QA and the gawd-danged manager who managed this freaking project!!!

Going back to the title of the article if you don’t know what the Galloping Gertie was, please check [this](http://www.youtube.com/watch?v=j-zczJXSxnw "The Galloping Gertie (Collapse of the Tacoma Narrows Bridge - Youtube Video)") out. If your site gets hacked (and I am not asking you to build an un-hackable site just don’t present it on a platter), and it turns out your users’ email and password were compromised and they were in plain text, your creation just collapsed like the Galloping Gertie. That single civil engineering ‘mistake’ is still upheld as how not to design a suspension bridge. It happened in the 1940’s and since then there have rarely been such spectacular bridge failures. But every second month we hear how a high profile site getting hacked and plain text passwords getting dumped for everyone to see. We don’t just seem to learn from our mistakes. Instead we crib, we crib about how little time we have to build/qa/test/gather requirements or how it is the platform’s fault blah blah blah! It’s always someone else’s mistake! STOP passing the buck it’s NOT someone else’s fault!!!

Sometime back I was reading in a blog (don’t remember the exactly where probably Hanselminutes), where it was said, health of a software development process is judged by how well the management knows about the code. Yes, you heard that right, the code. Unfortunately in the last twelve years I have seen people in software development, so eager to become managers so that they don’t have to look at code, that’s its sad! It’s beyond sad actually. When you have managers who don’t care about code, you have code that’s not the best it could have been because at the lowest level either the developer is too frustrated with writing the correct code or doesn’t care because they are in a hurry to become a manager too!!!

This happened closely in heel of the Path fiasco,  where a startup thought it was okay to upload the user’s entire address-book without asking and then pretended that it was a mistake. Free web, leaching out information from you in form of cookies was bad enough, now it is claimed that if a framework doesn’t stop me from reading other’s personal info it is an ‘industry-best-practice’ WTF!!! That’s like saying I built a virus because the OS allowed me to and I should be a hero!!!

Software Devs, it’s time we grew up and acted like grown ups. Take security and personal information more seriously. Be up-front about your actions to your end users, else software as a branch of engineering will be scarred irreparably!!!

**Update June 6, 2012:** It would seem another 'Galloping Gertie' has collapsed. **LinkedIn**'s database got compromised and revealed plaintext passwords. I guess going forth I'll just maintain this as a 'dis-honor roll' of sites getting hacked and being found to contain plaintext passwords. BTW according to their [blog](http://blog.linkedin.com/2012/06/06/linkedin-member-passwords-compromised/ "LinkedIn's blog")  they have 'recently' upgraded to salted hash passwords!
