---
layout: post
title: "Debugging iOS Binaries with LLDB (iOS 13) With Rejecting Incoming Connection Error"
date: 2020-02-12
author: Abbas Abdul Rahman
categories: [Security]
tags: [iOS]
description: This write up is a bruteforce work around I came up with in debugging iOS binaries using LLDB. 
---

This write up is a bruteforce work around I came up with in debugging iOS binaries using LLDB.  
Apple has done well to protect its technology stack so much so that even debugging external apps has a learning curve.  
To help with that, I have listed two articles that will be very helpful to anyone who wants to debug iOS apps for security testing or vulnerability research.

<!--more-->
[dima kovalenko]: https://kov4l3nko.github.io/blog/2016-04-27-debugging-ios-binaries-with-lldb/#run-a-binary-under-lldb
[felipe cavalcanti]: https://medium.com/@felipejfc/the-ultimate-guide-for-live-debugging-apps-on-jailbroken-ios-12-4c5b48adf2fb

For a full write up, refer to the articles below:

1. [Debugging iOS binaries with LLDB][dima kovalenko] by *Dima Kovalenko*.  
This post was written in 2016 targeting iOS 7 - 9 on ARM 32 and 64 bit processors.
2. [The missing guide to debug third party apps on iOS 12][felipe cavalcanti] by *Felipe Cavalcanti*.  
This post was written as recently as Aug 2019.

These articles will walk you through setting up debugserver and even getting up and running with  remote iOS debugger in IDA Pro.
The only problem is, these guides work up until the point where you try to hook lldb to a process listening on a port.  
See error on the last line of the image below.
{% include image.html
           image = "/img/2020/debug-ios-binary-1.png"
           title =
"Rejecting incoming connection"
           caption =
"Rejecting incoming connection."
%}. 
  
Above, I setup debugserver to accept a connection from any IP address so long as it was connecting over port 9999 to attach to a specific process id. The connection was rejected as shown in the image above with the error:

Error: rejecting incoming connection from ::ffff:192.168.1.224 (expecting ::1)

As can be deduced from the error, debugserver is rejecting a connection from 192.168.1.224, and was instead expecting a connection from ::1(the loopback address in IPV6 which equals 127.0.0.1 in ipv4). Therefore my lldb IP address was 192.168.1.224. Good.
We are making progress. At least I know if I supplied the localhost address, my connection should be accepted. Right?

I assumed lldb should be connecting from localhost and not 192.168.1.224. It wasn’t. Therefore connections from lldb were still being rejected. So I specified 192.168.1.224 to be the IP address debugserver should be expecting a connection from. That way, when lldb reaches out to debugserver, it presents it’s address as 192.168.1.224 and since debugserver is already expecting that IP address: BOOM. CONNECTED and DONE. See below.
{% include image.html
           image = "/img/2020/debug-ios-binary-2.png"
           title =
"Successful connection"
           caption =
"The debugserver is no more rejecting connection."
%}. 

`lldb` is now able to connect to the debugserver.
{% include image.html
           image = "/img/2020/debug-ios-binary-3.png"
           title =
"lldb can reach the debugserver now"
           caption =
"lldb can reach the debugserver now."
%}. 

`Happy debugging!!!`
