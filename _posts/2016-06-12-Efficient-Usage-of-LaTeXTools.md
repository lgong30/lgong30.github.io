---
layout: post
title: LateXTools for Cross Reference in Multi-file LaTeX Projects
tags: [LaTeXTools, sublime]
categories: [skill]
---

In this post, we will introduce a method to help you easily do cross reference in a multi-file latex project (_i.e._, a latex project where latex source files are distributed into multiple files). For example, the file structure of a multi-file latex project might look like:

```shell
path/to/your-latex-project/
    main.tex 
    introduction.tex
    related-work.tex
    my-work.tex
    evaluation.tex
    conclusion.tex
    reference.bib
    figures/
```

In the above project, you might cross cite for example an algorithm which you define in the file `my-work.tex` in the file `evaluation.tex`. Without the assistance of some useful tools, you might have to check the file `my-work.tex` to make sure which label you have defined for that algorithm. And in some tools, they might automatically remind you all the labels you have defined in the current file, which means they cannot help you in the cross-file cross reference. 

In this post, we will describe you an easy method to help you do the cross-file cross reference by using the [**LaTeXTools**](https://github.com/SublimeText/LaTeXTools) plug-in of [**Sublime Text**](https://www.sublimetext.com/). Note that in this post, we will focus on the configuration for cross-file cross reference. If you have no idea on how to install the LaTex Tools or even Sublime Text, please ask Google or some other search engine. 

Create a Sublime Text Project
-----------------------------

Create a sublime text project for your multi-file latex project. If you have no idea on how to create a project in sublime text 2/3, please refer to [understanding-projects-in-sublime-text-saving-switching-etc](http://www.joshuawinn.com/understanding-projects-in-sublime-text-saving-switching-etc/). 

Configure Your Project
----------------------

After you create your project, you will see a auto-created file (named as `your-project-name.sublime-project`) in your root path of your multi-file latex project. Open the file, and the put the following configurations into the file. 

```json
"settings" : {
    "TEXroot": "main.tex",
    "tex_file_exts": [".tex"]
}
```

The above configuration assumes, the root latex file of your project is `main.tex` (if your project use another tex file, please change it correspondingly.). If you really want to make a full understanding of the above configurations, please refer to [Project-Specific Settings](https://github.com/SublimeText/LaTeXTools#settings) of the Latex Tools.

The following is for those who are not so familiar with **JSON**, _i.e._, the format for the project setting file. Usually, before you do manual changes on the project setting file, its content looks as follows:

```json
{
    "folders":
    [
        {
            "path": "."
        }
    ]
}
```


After you add the configurations, your setting file would look as follows (please pay attention to the comma after the `]`, it cannot be omitted):

```json
{
    "folders":
    [
        {
            "path": "."
        }
    ],
    "settings" : {
        "TEXroot": "main.tex",
        "tex_file_exts": [".tex"]
    }
}
```

Please pay attention to the **comma** added after the close square bracket (__i.e.,__ `]`).


Notice
------

If you have any suggestions or questions regarding this post, please lease your message in the comment session or send e-mail to <mailto:mr.gonglong@outlook.com> directly.