---
layout: post
category: "Editer"
title: "Using LaTeX to pdf in sublime text3 "
tags: ["sublime","latex","PDF","IDE"]
---

### 安装sublime text3
{: #top}

如果使用ubuntu，可以参考我之前写的文章[ubuntu_sublime_text](http://wdyggh.github.io/ubuntu/ubuntu_sublime_text.html)。  
如果使用windows的话安装也很简单，另外也没有中文输入的麻烦。  
就贴上官网链接吧 sublime text3 homepage [^1]。  
另外安装 `package control` 也是必须的。  
本文主要针对 `windows` 的用户，如何使用sublime进行latex编辑，包括数学公式preview，以及导出pdf。  

### 安装 LaTeX 环境

LaTeX 环境有有几种，这里使用 `MiKTeX` ，到官网 [^3] 下载安装就行。 


### 安装 `SumatraPDF`

SumatraPDF [^2] ,下载安装 并添加安装路径到 `PATH` 。

为了实现反向搜索：在SumatraPDF中双击要修改的地方，在sublime中光标会移动到对应的位置。需要在SumatraPDF中设置 > 选项。  
找到自己安装sublime text的位置 `替换` 。  

> "C:\Program Files\Sublime Text 3\sublime_text.exe" "%f:%l"

![sumatraPDF_Setting](http://7xifyp.com1.z0.glb.clouddn.com/sumatraPDF_Setting.PNG){: .max-height-image}  

### 安装 `imagemagic` 和 `ghostscript`

imagemagic homepage[^4]    
ghostscript homepage[^66]  
完成安装之后，同样添加安装路径到 `PATH` 。

### 安装 `LaTeX Tools` 和设置

使用sublime text 中的 LaTeX Tools 插件带来语法高亮，和及时公式preview。  
及时公式preview 对于写论文的同学来讲，是个利器之一。  
输入 Ctrl+Shift+p > package control install > latex tools 完成安装。  

在sublime text 中完成 math preview 的设置：  
Preferences > Package Settings > LatexTools > Settings - User  

```
"preview_math_mode": "selected",
"preview_math_scope": "text.tex.latex meta.environment.math",
```

到这大概完成了90%，剩下的需要 在sublime text 中 Ctrl+Shift+p > `latex tools: check system` 来确认还有哪些需要安装。
等结果出来后，可能显示所有项目都已经安装好了，显示为`available`,但在编辑latex 公式的时候，还不能preview，并显示error message。那就说明有些 LaTeX package 没有安装好，我就碰到了全部显示 available ，然而还是不能preview的情况。最终在google之后找到了答案 [github_latexTools_Issue](https://github.com/SublimeText/LaTeXTools/issues/920#issuecomment-258598688)。  
新建并编译(`ctrl+B`)以下文档，MiKTeX 会安装缺失的package。此时鼠标再移到有公式的地方就会自动实现math preview。  


```latex
\documentclass[preview]{standalone}


% import xcolor if available and not already present
\IfFileExists{xcolor.sty}{\usepackage{xcolor}}{}%

% The four packages below are specified in LatexTools.sublime-settings
\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{latexsym}
\usepackage{mathtools}
%<<preamble>>
\begin{document}
% set the foreground color
%\IfFileExists{xcolor.sty}{<<set_color>>}{}%
$$
a = b
$$

\end{document}  
```

![sublime math preview](http://7xifyp.com1.z0.glb.clouddn.com/sublime_math_preview.PNG){: .max-height-image}



#### *Reference:*  

1. [ubuntu_sublime_text](http://wdyggh.github.io/ubuntu/ubuntu_sublime_text.html)  
2. [github_latexTools_Issue](https://github.com/SublimeText/LaTeXTools/issues/920#issuecomment-258598688)
3. [使用 Sublime Text 编辑和编译 LaTeX 文档](http://www.jianshu.com/p/51ae1bb01885)

- - - 

### [TOP](#top)

#### *Footnote:*

[^1]: [sublime_text3_homepage](https://www.sublimetext.com/)
[^2]: [SumatraPDF](https://www.sumatrapdfreader.org/free-pdf-reader.html)
[^3]: [MiKTeX](https://miktex.org/)
[^4]: [imagemagick](https://www.imagemagick.org/script/index.php)
[^66]: [ghostscript](https://www.ghostscript.com/)