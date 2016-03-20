---
title: Github+Hexo搭建个人博客
date: 2016-03-19 17:03:02
tags: [others,github,hexo,SSH]

---
# 1.安装环境
Git --我开始用的是2.7，但是发布经常出问题，换回1.9就没问题了(折腾了很久)
Nodejs --我用的是5.9没有发现问题

# 2.安装步骤
``` 
npm install -g hexo-cli    //安装主程序
cd blog                    //我自己定义了一个叫blog的文件夹，然后进入这个文件夹
hexo init                  //初始化 hexo 产生工程文件
npm install                //安装一些必要的插件
npm install hexo-deployer-git --save    //这个也最好安装一下，避免以后deploy失败
```
# 3.配置config.yml文件
在根目录（blog文件夹内）
``` 
deploy:
  type: git
  repository: https://github.com/pengweb/pengweb.github.io.git
  branch: master
```
写成https的格式的话，我跑在git1.9上是没问题的，但是在2.7上就报错了
还有一种是使用SSH地址：我在下边有详细些SSH配置
```
deploy:
  type: git
  repository: git@github.com:pengweb/pengweb.github.io.git
  branch: master
```
这里用的是SSH地址，同样我跑在git1.9上是没问题的，但是在2.7上就报错了
# 4.创建新文章
```
hexo new 文章名
```
创建好后可在source\_posts下找到  文章名.md 文件 对齐进行编辑就行了

# 5.清理一下缓存---推荐
```
hexo clean
```
# 6.生成静态页面
```
hexo generate    //简写 hexo g
```
# 7.进行本地预览
```
hexo server      //简写 hexo s
```
# 8.发布到github上
```
hexo deploy      //简写 hexo d
```
# 9.除了可以新建文章也可以新建一个页面
```
hexo new page 页面名
```
# 10.SSH配置详解
## 10.1 打开ssh目录
一般都是隐藏的
```
cd ~/.ssh
```
或者去直接找到这个文件夹在
```
C:\Users\计算机名\.ssh
```
## 10.2 生成密钥文件，默认名字为id_rsa和id_rsa.pub
```
ssh-keygen -t rsa -C "YOUR_EMAIL@YOUREMAIL.COM"
```
*说明：换成你自己的邮箱*
**不要改名字，就用id_rsa和id_rsa.pub，我改过几次，都以失败告终，但是按理说是可以的**
## 10.3 打开公钥文件（id_rsa.pub），并把内容复制至代码托管平台上
settings→SSH keys
## 10.4 测试
```
ssh -T git@github.com
```
*成功提示：Hi xxxxxx! You've successfully authenticated, but GitCafe does not provide shell access.*
# 11.主题安装
## 11.1 切到主题目录下
```
 cd themes
```
## 11.2 下载主题
```
git clone https://github.com/foreachsam/hexo-theme-monogatari
```
## 11.3 修改config.yml文件
```
theme: hexo-theme-monogatari      //没有的话就直接添加上就可以
```
## 11.4 更新主题
```
cd hexo-theme-monogatari
git pull
```
## 11.5 主题的config.yaml文件配置--目录
```
	HOME: /
  Javascript: /tags/javascript
	Sitemap: archives
```
*书写的对齐方式也很重要，我在Sublime里看就是左对齐的，但是webstrom就是第二项比其他提前一个tab，我对齐了，却报错了*
# 12.多说评论框
## 12.1 配置config.yml
```
duoshuo_shortname: 你站点的short_name
```
*这里的你站点的short_name指的是多说分配给你的二级域名前边那个你自己设定的name，不包含后边的网址，只是name*
## 12.2 配置模板文件
``` 
<% if (config.duoshuo_shortname){ %>
  <section id="comments">
    <!-- 多说评论框 start -->
    <div class="ds-thread" data-thread-key="<%= path %>" data-title="<%= title %>" data-url="<%- link %>"></div>
    <!-- 多说评论框 end -->
    <!-- 多说公共JS代码 start (一个网页只需插入一次) -->
    <script type="text/javascript">
    var duoshuoQuery = {short_name:'<%= config.duoshuo_shortname %>'};
      (function() {
        var ds = document.createElement('script');
        ds.type = 'text/javascript';ds.async = true;
        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
        ds.charset = 'UTF-8';
        (document.getElementsByTagName('head')[0] 
         || document.getElementsByTagName('body')[0]).appendChild(ds);
      })();
      </script>
    <!-- 多说公共JS代码 end -->
  </section>
  <% } %>
```
 *一般出错都处在data-thread-key="<%= path %>" data-title="<%= title %>" data-url="<%- link %>"这几个配置值上，这个是我这个模板的，具体指什么，多说初始让你粘贴的代码里有解释，不做赘述*
# 13.favicon.ico
这个放在根目录下（source）下
下边这个config.yml配置可以不配置
```
# Place your favicon.ico to /source directory.
favicon: /favicon.ico
```
# 14.404页
``` html

---
layout: default
---
<html>
    <head>
         <meta charset="UTF-8" />
         <title>404</title>                                                                                                                                        
    </head>
    <body>
         <script type="text/javascript" src="http://www.qq.com/404/search_children.js" charset="utf-8"></script>
    </body>
</html>
```
