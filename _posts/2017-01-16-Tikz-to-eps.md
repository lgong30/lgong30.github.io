---
layout: post
title: TikZ to eps
categories: [skill]
tags: [latex]
---

TiKz provides a very efficient way for us to "program" our figures. However, sometimes you might only want to share your figures but not the source codes of your figures with other for some reasons (_e.g.,_ the source code uses a large amount of TiKzlibrary, other people might not have these libraries in the machine or you just want to make your codes private). In this post, we present a way to generate eps figure from TikZ source code (Of course, you can also generate a PDF and let others include that PDF).



LaTeX Code
----------

```TeX
\documentclass{article}

\usepackage{tikz}

%% put tikzlibrary below if necessary

% set up externalization
\usetikzlibrary{external}
\tikzset{external/system call={latex \tikzexternalcheckshellescape -halt-on-error
-interaction=batchmode -jobname "\image" "\texsource";
dvips -o "\image".ps "\image".dvi;
ps2eps "\image.ps"}}
\tikzexternalize

\begin{document}

%% put your tikz code below or input your tikz code via \input


\end{document}
```

Usage
-----


```shell
latex -shell-escape LATEX_FILE_NAME
```

Please make sure you are using `latex` engine, other engines
will not work. Besides, please make sure all required tools
are installed.
