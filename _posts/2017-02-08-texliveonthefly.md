---
layout: post
title: Automatically Install Dependent Packages For Your BasicTex
categories: [gadgets]
tags: [programming, LaTeX]
code: /TexliveOnTheFly
---

If you are using BasicTex on your Mac, you might get frustrated when you get errors on missing packages, especially when the latex source using too many packages that you did not install on your Mac. Is there any tools that could help you automatically install those missing packages. YES! [texliveonfly](https://www.ctan.org/pkg/texliveonfly?lang=en) provides you such capability. However, you might want this feature to be integrated into your text editor such as [Sublime Text](https://www.sublimetext.com). 

In this post, we help you design a sublime text plugin for supporting `texliveonfly`.


Usage
-----
Press `cmd+shift+f` (unfortunately, current version needs you start your sublime text with the privilege of a superuser, in the future, we will try to figure out how to avoid this)

Installation
------------
`git clone https://github.com/lgong30/TexliveOnTheFly ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/TexliveOnTheFly`


TODO
----
+ Provide customization feature
+ Avoid the requirement for super user privilege
