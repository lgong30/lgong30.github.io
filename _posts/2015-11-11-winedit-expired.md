---
layout: post
title: Get Rid of WinEdit Expired Problem
tags: [latex, WinEdit]
categories: [skill]
---


As a convenient editor for TeX file under Windows, [WinEdit](http://www.winedt.com/) is quite popular. However, if you do not get your 
WinEdit registered (of course, it is not free), you will get annoyed 
by the popup window, which gets appeared frequently after you have 
used WinEdit without registration for certain time period. This post 
provides a hack way to deal with it. 




Find Configuration File "Exit.edt"
----------------------------------

options -> options interfaces ... -> Advanced Configuration ... -> Event Handlers -> Exit

the file looks like this:


```shell
// WinEdt Exit (Cleanup) Macro
 
   PushTagsandRegisters;
 
//  CloseAppl("YAP");         // Close YAP if running?
//  CloseAppl("Complete");    // Close Complete Wizard if running?

// Remove Local ini and edt files if they are empty or the same as global
// Users probably forget to do this before upgrading
// so it is best to keep it tidy as we go...

Exe('%b\Config\Cleanup.edt');

PopTagsandRegisters;

End; 
```


Add Following Sentence Just Before **"End;"** 
---------------------------------------------

    RegDeleteValue('HKEY_CURRENT_USER', 'Software\WinEdt 9', 'Inst');

Not sure whether it works for WinEdit 10.


Close WinEdit and Reopen
------------------------



Notice
------

Note that, we do not recommend you to use this solution. If you really 
cannot afford the registration, then [Sublime Text](https://www.sublimetext.com/) together with [LaTeXTools](https://github.com/SublimeText/LaTeXTools) would be a good conditionally free substitute. Tis 
installation and configuration of Sublime Text with LaTeXTools can be 
found in [Play LaTeX Projects with Sublime Text 3](https://lgong30.github.io/skill/2016/09/16/sublime-text-3-latextools.html).


  


