---
layout: post
category: "ubuntu"
title: "ubuntu 小技巧"
tags: ["ubuntu"]
---


### Tips 持续更新

<a name="top"></a>
* ###1 添加`韩语输入法`
    在google上寻找了好半天，只看到了`ibus`的方法，大概如下吧：

    ```bash
    sudo apt-get instal ibus-hangul
    ```

    然后我用的是`fcitx`，然后依葫芦画瓢，有了如下的命令：

    ```bash
    sudo apt-get install fcitx-hangul 
    ```

    结果还有用了，不过前提是得先安装好`fcitx`

* ###2 安装 `Adobe Reader`
    pdf的话自带的文档查看器已经能满足基本需求了，  
    但是在windows上的习惯，  
    不装个Adobe Reader 试试，是不会甘心的。   
    下面就教你如何安装 Adobe Reader：    
    添加库：    

    ```bash
    sudo add-apt-repository "deb http://archive.canonical.com/ precise partner"
    ```

    然后执行更新和安装：

    ```bash
    sudo apt-get update
    sudo apt-get install acroread
    ```

    再移除 远程库：  

    ```bash
    sudo add-apt-repository -r "deb http://archive.canonical.com/ precise partner"
    sudo apt-get update
    ```

    设置默认打开软件：   
    在`pdf`文件上右击`属性(P)`> 打开方式 > 找到Adobe Reader >设为默认值就ok啦

* ### 3 下载软件 `uGet`
    去[官网](http://ugetdm.com/downloads-ubuntu)下载，   
    选择对应的ubuntu版本号，还有x86-64|i386   

    官网上也有指导用命令行安装的：  

    ```bash
    sudo add-apt-repository ppa:plushuang-tw/uget-stable
    sudo apt update
    sudo apt install uget
    ```

    在ubuntu软件中心里搜索`uGet`也能安装。





- - - 

###[TOP](#top)
