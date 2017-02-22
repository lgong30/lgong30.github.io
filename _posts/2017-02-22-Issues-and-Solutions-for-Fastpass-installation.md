---
layout: post
title: Installation of Fastpass -- Issues and Solutions
categories: [skill]
tags: [DC networking]
---

[_Fastpass_](http://fastpass.mit.edu/) is a datacenter network framework proposed by Jonathan Perry, _et al._. Its authors published its codes, however, I encountered some issues while installing it on Ubuntu 16.04.

+ Issue 1: gcc version issue 
  - error: `include/linux/compiler-gcc.h:86:30: fatal error: linux/compiler-gcc5.h: No such file or directory`
  - cause: the kernel version of my Ubuntu (_i.e.,_ Ubuntu 16.04) is higher than the kernel version used by fastpass (_i.e.,_ v3.10.25).
  - solution: before `make -j22` adding `echo "#include <linux/compiler-gcc4.h>" > include/linux/compiler-gcc5.h`
  - source: [compile-a-linux-2-6-kernel-module-with-newer-compiler](http://stackoverflow.com/questions/29925513/compile-a-linux-2-6-kernel-module-with-newer-compiler)
+ Issue 2: Berkley DB issue
  - error: 

    ```shell
    E: Unable to locate package libdb6.0-dev
    E: Couldn't find any package by glob 'libdb6.0-dev'
    E: Couldn't find any package by regex 'libdb6.0-dev'
    ```
  - cause: it seems there is no package `libdb6.0-dev` for Ubuntu 16.04 (I only found `libdb6.0-dev` for Ubuntu 14.04)
  - solution: replace `libdb6.0-dev` with `libdb-dev` (if you still see the similar error, then you might need add the [source](http://packages.ubuntu.com/xenial/amd64/libdb-dev/download) to your `/etc/apt/source/lsit` )
