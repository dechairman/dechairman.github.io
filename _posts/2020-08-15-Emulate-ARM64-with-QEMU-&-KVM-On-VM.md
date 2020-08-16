---
layout: post
title: "Emulating ARM64 with QEMU/KVM on a Debian guest VM"
date: 2020-08-15
author: Abass Abdul-Rahaman
categories: [Security]
tags: [Linux]
description: This write up describe how to emulate arm64 on a VMware box.
---

[QEMU]:https://en.wikipedia.org/wiki/QEMU
[KVM]:https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine

[QEMU](Quick EMUlator) is an open source emulator and virualization sofware that can perform hardware virtualization. 
When used with [KVM], virtual machines can run at near native speed. There are write up's on how to run QEMU on macOS, windows and linux.
I wanted to emulate the ARM64 architecture using QEMU and KVM. Since I didn't have a computer hardware running linux, I wanted to try running a 
guest debian box and use QEMU/KVM to emulate the arm64 arch. This makes for nested virtualization which is not ideal for speed and efficiency if you want 
to run a full desktop VM. In my case, all I wanted to do was debug the linux kernel on an arm64 arch.

<!--more-->
