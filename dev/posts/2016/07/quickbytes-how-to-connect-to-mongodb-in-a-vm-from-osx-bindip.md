---
author: "Sumit"
title: "Quickbytes: How to connect to MongoDB in a VM, from OSX (bindIP)"
date: "2016-07-29"
categories: 
  - "linux"
  - "mongodb"
  - "os"
  - "osx"
---

I like to keep my base system clean of databases and web-servers etc. So when I wanted to play around with MongoDB on my laptop instead of cluttering it up, I setup a little Virtual Box VM running Debian 8.5 and got MongoDB 3.2 on it in a jiffy using the official docs.

I then installed my favourite MongoDB client Robomongo and was all set to connect to the DB in the VM itself.

But when I installed Robomongo on OSX it just wouldn't connect to the VM. I assumed its getting blocked by default OS settings on Debian. So I updated the IP Tables as follows

sudo iptables -A INPUT -s 192.168.0.42 -p tcp --destination-port 27017 -m state --state NEW,ESTABLISHED -j ACCEPT

This enables incoming connections to port 27017, MongoDB default port.

sudo iptables -A OUTPUT -s 192.168.0.42 -p tcp --source-port 27017 -m state --state NEW,ESTABLISHED -j ACCEPT

This enabled outgoing connections.

Replace \[192.168.0.42\] with IP address of you machine/laptop on which the VM is hosted.

I assumed this would be enough but nope. Robomongo on OSX kept refusing to connect with the error "Network is not reachable". After running up lots of wrong trees I finally found out that MongoDB forces local IP binding by default as a security measure. This setting is in /etc/mongod.conf

net:

port: 27017

bindIp: 127.0.0.1

I changed the bindIp to \[127.0.0.1,192.168.0.42\]. Final settings were:

net:

port: 27017

bindIp: \[127.0.0.1,192.168.0.42\]

Save the conf, restart mongodb service and Bazinga!

Quick vote of thanks to the following articles:

https://tanzimsaqib.wordpress.com/2015/06/12/installing-and-securing-mongodb-on-windows-linux-on-azure/

http://stackoverflow.com/questions/17588876/mongodb-conf-bind-ip-127-0-0-1-does-not-work-but-0-0-0-0-works

Security Note: Setting bindIP to 0.0.0.0 is the worst move from a security point of view. Do not do it!
