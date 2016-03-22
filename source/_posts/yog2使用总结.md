---
title: yog2使用总结
date: 2016-03-21 23:05:28
tags: [others,yog2]

---
一、找到想放工程的目录然后


<blockquote>yog2 init project</blockquote>


输入后提示创建工程名字
来创建一个项目的工程目录

二、进入创建的工程目录内创建自己app的目录


<blockquote>yog2 init app</blockquote>


输入后提示创建app名字（app-zhp）

三、更新依赖（工程目录下）


<blockquote>npm install</blockquote>


四、启动框架（工程目录下）


<blockquote>yog2 run</blockquote>


(默认端口我8085，可以通过修改PORT或者app.js来修改端口，访问地址为127.0.0.1：8085)

五、部署app（在app目录下）


<blockquote>由于启动框架占用了控制台，所以需要再打开一个控制台来部署app
yog2 release --dest debug</blockquote>


再次访问127.0.0.1：8085就可以正常提供服务了，如果想切换app

注意：同时添加--watch，就可以监听前后端修改，并部署到project中


<blockquote>yog2 release --dest debug --watch</blockquote>

