---
layout: post
title: Simple PDF Merger
categories: [gadgets]
tags: [programming, gui]
code: /pdfMerge
---

PDF has become one of the most popular file type used on our electronic devices.
However, the management of PDF files is not an easy task, especially when you have too many PDF files. For example,
as a undergraduate/graduate student, you might obtain bunch of lectures in PDF format for a certain course (say _Calulus_). After you have taken this course for a long while, we encountered some concepts in Calculus, but you did not remember the details behind them. However, you are $100%$ sure that they must be in certain lectures (but you are not sure which lectures they locate in). At this time, you might want a tool to combining these lectures into a single file such that you can easily locate them. 


In this post, we introduce a simple tool that can provide you a user-friendly GUI to combine multiple PDF files into a single one. 


Dependencies
------------
+ PyPDF2
+ Tkinter

**Remarks**: In the future, to support _drag and drop_, we might switch to Java.


Usage
-----
+ Clone from Github: `git clone -b gui https://github.com/lgong30/pdfMerge`
+ Go to the repository: `cd pdfMerge`
+ Install dependencies: `pip install -r requirements.txt` (Note that, if you get _permission denied_ errors, please add a `sudo` before `pip`)
+ Give the python script the permission to execute: `sudo chmod +x window.py`
+ Run: `./window.py`


TODO
----
- Add per-file bookmarks while merging
- Improve the "look" of this application
- Add the support for drag-and-drop 









