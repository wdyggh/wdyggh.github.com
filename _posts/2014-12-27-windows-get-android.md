---
layout: post
category: "android"
title: "Windows下载Android源码之路"
tags: ["android", "源码"]
---
####1、准备工作
安装git（已自带cygwin）；Python2.7.8并配置到环境变量；VPN稳定可用。  

####2、下载repo并配置到环境变量
	curl https://storage.googleapis.com/git-repo-downloads/repo > repo
	chmod a+x repo
	
####3、创建源码存放目录，并执行下载
	mkdir source
	cd source
	repo init -u https://android.googlesource.com/platform/manifest -b android-4.4.4_r2.0.1
	repo sync

####4、等待下载完成
其它操作。