---
title: Github+Hexo搭建个人博客
date: 2016-03-19 17:03:02
tags: [others]
---
#安装环境
Git --我开始用的是2.7，但是发布经常出问题，换回1.9就没问题了(折腾了很久)
Nodejs --我用的是5.9没有发现问题

#安装步骤
```
npm install -g hexo-cli    //安装主程序
cd blog                    //我自己定义了一个叫blog的文件夹，然后进入这个文件夹
hexo init                  //初始化 hexo 产生工程文件
npm install                //安装一些必要的插件
npm install hexo-deployer-git --save    //这个也最好安装一下，避免以后deploy失败
```
#配置
在根目录（blog文件夹内）