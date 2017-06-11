---
layout: post
title: Play Against .gitignore With Sublime Text Plugin
categories: [tool]
tags: [sublime text, gitignore]
---

If ever played with GIT, then you might encountered a tedious situation, where you need create a `.gitignore` file for every repository even if many of your repositories share the same `.gitignore` file. Some of you might have stored these `.gitignore` files for various projects, however, the manual copy and paste are still tedious. Are there any tools that can help us "play against" `.gitignore` easier? In this post, we will introduce you one of such tools.

Requirements
------------
+ [Sublime Text](https://www.sublimetext.com)
+ [Sublime-Gitignore](https://github.com/theadamlt/Sublime-Gitignore)

Install & Usage
---------------

Please refer to the corresponding "official site" of [Sublime Text](https://www.sublimetext.com) or [Sublime-Gitignore](https://github.com/theadamlt/Sublime-Gitignore).


Customization
-------------

Of course, the template provided in [Sublime-Gitignore](https://github.com/theadamlt/Sublime-Gitignore) might not satisfy your requirements. Then, you can customize the templates. Before that, you need another sublime text plugin (at least for sublime text 3), that is [PackageResourceViewer](https://github.com/skuroda/PackageResourceViewer). 

+ First, you need extract the package `Sublime-Gitignore` (HOWTO: please refer to the "official site" of [PackageResourceViewer](https://github.com/skuroda/PackageResourceViewer))
+ Second, dive into the directory of all templates in `Sublime-Gitignore` (_i.e.,_ the sub-directory `boilerplates` under the root directory of package `Sublime-Gitignore`)
+ Third, create or edit the corresponding `.gitignore` template


