---
layout: post
category: "android"
title:  "用git进行分支开发、合并主要流程"
tags: [git]
---
####1、克隆远程版本库。
git clone git@github.com:youth168/test.git  
输入密码:git，等待完成。  
cd ./test

####2、建立目标分支进行开发
git checkout -b dev-branch master  
经过对本地dev-branch开发后...  
git add .  
git commit -am "feature adding and bugs fixing"

####3、合并本地分支(dev-branch)到master分支
git checkout master  
git push origin master

####4、再对dev-branch开发
git checkout dev-branch  
再重复第3步...

####5、本地dev-branch删除
不再基于dev-branch开发了，删除之  
git branch -d dev-branch

####6、设置Tag(快照)
git tag v1.0 '新建本地tag  
git tag -d v1.0 '删除本地tag  
git push --tag 'push本地tag到远程  
git push origin --delete tag v1.0 '删除远程tag  

注：基于远程子分支开发同以上操作。