
---
layout: post
title: "Debugging iOS Binaries with LLDB (iOS 13) With Rejecting Incoming Connection Error"
date: 2020-02-12
author: Abbas Abdul Rahman
category: Security
tags: [iOS]
description: > This write up is a bruteforce work around I came up with in debugging iOS binaries using LLDB. 
Apple has done well to protect its technology stack so much so that even debugging external apps has a learning curve.
---

This write up is a bruteforce work around I came up with in debugging iOS binaries using LLDB.  
Apple has done well to protect its technology stack so much so that even debugging external apps has a learning curve.  
To help with that, I have listed two articles that will be very helpful to anyone who wants to debug iOS apps for security testing or vulnerability research.  
For a full write up, refer to the articles below:

[Debugging iOS binaries with LLDB](https://kov4l3nko.github.io/blog/2016-04-27-debugging-ios-binaries-with-lldb/#run-a-binary-under-lldb by *Dima Kovalenko*.  
This post was written in 2016 targeting iOS 7 - 9 on ARM 32 and 64 bit processors.
[The missing guide to debug third party apps on iOS 12] by *Felipe Cavalcanti*. This post was written as recently as Aug 2019.

These articles will walk you through setting up debugserver and even getting up and running with  remote iOS debugger in IDA Pro.
The only problem is, these guides work up until the point where you try to hook lldb to a process listening on a port.  
See error on the last line of the image below.
