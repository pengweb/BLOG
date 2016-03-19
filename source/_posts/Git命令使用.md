---
title: Git命令使用
date: 2016-03-19 17:27:09
tags:
---
#1.创建本地仓库
直接在github上创建仓库比较简单不做描述。
```
//创建一个要同步文件夹，并且进入这个文件夹
git init //初始化git
git add . //将文件夹内的所有文件放到暂存区，注意点之前有空格
git commit -a -m '这里写的是备注' //提交所有（m）更新过的文件, -a是所有更新过的文件
git remote add orign git@github.com:pengweb/BLOG.git   //关联到github上，此时并没有在github上创建呢，只是关联上了
git push orign -u origin master  //这样就推送上去了，这里的u为了让本地分支也关联到远程服务器上的分支