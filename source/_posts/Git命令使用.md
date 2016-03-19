---
title: Git命令使用
date: 2016-03-19 17:27:09
tags: [others]
---
[TOC]
#1.创建本地仓库

``` bash
//创建一个要同步文件夹，并且进入这个文件夹
git init //初始化git
git add . //将文件夹内的所有文件放到暂存区，注意点之前有空格
git commit -a -m '这里写的是备注' //提交所有（a）更新过的文件, -m是备注
```
# 2.发送到远程服务器
``` js
//如果要想传到github上，先在github上创建一个仓库，然后执行下边指令
git remote add origin git@github.com:pengweb/BLOG.git   //关联到github上，此时并没有在github上创建呢，只是关联上了
git push -u origin master  //这样就推送上去了，这里的u为了让本地分支也关联到远程服务器上的分支
```
# 3.更新中···