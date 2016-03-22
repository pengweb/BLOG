---
title: Git命令使用
date: 2016-03-19 17:27:09
tags: [others，git,github]

---
# 1.创建本地仓库
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
# 3.去除远程子模块
``` bash 
//清除缓存区-单独文件
git rem --cached theme/
//清除缓存区-全局
git reset HEAD
```
# 4.远程公共自模块submodule
``` bash
//为当前工程添加submodule
git submodule add 仓库地址 路径
//删除  --  执行下边命令后还要对.gitmodules文件和git中进行删除
git rm –cached 
//下载的工程含有submodule，进行更新
git submodule update --init --recursive