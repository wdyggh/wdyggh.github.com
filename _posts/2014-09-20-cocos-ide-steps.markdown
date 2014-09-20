---
layout: post
category: "cocos2d"
title:  "Cocos IDE开发步骤"
tags: [Cocos2d IDE]
---
####一、启动Preferences设置
1、General中设置Cocos2d-JS路径.  
2、设置Python，SDK,NDK,ANT,JDK路径。  
3、运行工程，run as...（同Android)。  

####二、开发
1、添加图片等到res目录下，并在src/resources.js中注册。  
2、添加js文件到src目录下，并在project.json中注册到jsList数组中。  

####三、命令行模式
1、新建：cocos new MyGame -l js  
2、运行：cocos run -p web|android|ios  

Cocos2d-JS官网：<http://cocos2d-x.org/wiki/Getting_Started_Cocos2d-js>  

（完~）