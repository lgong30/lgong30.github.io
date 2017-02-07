---
layout: post
title: Make High-Quality EPS File with Visio
tags: [visio, eps]
categories: [skill]
---

EPS figures are very important to scholars. However, making eps figures, especially high-quality ones is not an easy task. Today, we will introduce a simple method easily finish this tough task with visio.


Tools are needed
----------------

1. [Visio](http://pan.baidu.com/s/1gd0G0EZ)
2. [Adobe Acrobat](http://pan.baidu.com/s/1CvVJo)
3. [GSView](http://pan.baidu.com/s/1wMRvC)

HOWTO
-----

1. Use **Visio** to draw a figure (__i.e.__, the figure to be transformed to eps)

2. Print this figure to **PDF** format in **Visio** by using **Adobe Acrobat Printer**. **Note that**, make sure your figure is located in a single page, and you are suggested to use high-quality printer.

3. Open the PDF generated in **Step 2** by using **Adobe Acrobat**, and **saveas "eps"**. **Note that**, though you obtain the eps file already in this step, but usually this file could not satisfy your requirement. Therefore, you need still come to **Step 4**.

4. Open the EPS generated in **Step 3** by using **GSview**, and then **"File"/"PS to EPS"**, **check** "Automatically calculate Bounding Box" if it isn't, and then press "Yes". Eventually, you get the desired EPS figure.


Notice
------

If your figure is very regular (with only certain regular-shape stuffs, for example a combination of rectangles/circles/lines.), `Tikz` might be a very good tool for producing eps figures. [This repository](https://github.com/xlong88/LaTeX-examples/tree/master/tikz) provides some useful examples. If you want more, if can go to [TeXample.net](http://www.texample.net/tikz/examples/). In the future, we will provide some specific examples which we 
encountered in some of our projects.
