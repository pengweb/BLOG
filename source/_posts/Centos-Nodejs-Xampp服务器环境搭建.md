---
title: Centos+Nodejs/Xampp服务器环境搭建
date: 2016-03-21 22:11:49
tags: [centos,linux,nodejs,xampp,服务器]

---
<h3>Linux配置:</h3>

<h4>首先配置虚拟机</h4>

编辑-虚拟网络编辑器-修改vmnet0为桥接模式
虚拟机-设置-网络适配器-修改为桥接模式

<h4>配置Linux文件</h4>
cd ..   先返回根目录
cd etc/sysconfig/network-scripts
vi ifcfg-eno*    修改这个文件*是不同Linux版本这个尾号不同，自己查
将内容改为如图下
![](/images/11111.jpg)
里边很多配置可以不用，可以自行百度

修改域名服务器-避免ping不通网址
cd etc/resolv.conf
添加下边这个
<pre>
nameserver 8.8.8.8
nameserver 8.8.4.4
</pre>


安装epel-因为Linux自己的yum发行版不全，所以通过这个扩展
<pre>
yum install epel-release
</pre>



<h3>安装NodeJS:</h3>

<pre>
yum install nodejs
</pre>


<h3>安装Xampp:</h3>

<blockquote>cd /home
cd /zhp
cd Desktop
chmod a+x xampp```````.run
sh 文件名-这个不能执行-直接输入文件名也不能执行
./文件名 执行安装
ls当前文件夹
su - 获取权限
cd -返回上一级目录</blockquote>
每次执行：
<blockquote>cd /opt
cd lampp
sudo ./manager-linux-x64.run</blockquote>



<h3>配置子目录多站点:</h3>


经常需要在本地调试网站，却又不喜欢在<a href="http://localhost/">http://localhost/</a>网站的文件夹名，且几个比较重要的项目我想直接用端口号以示区分，想达到的效果如下：
<a href="http://localhost/">http://localhost/</a>     默认80端口的时候访问的是D:\目录下的A网站
<a href="http://localhost:8080/">http://localhost:8080/</a>    8080端口的时候访问的是E:\目录下的B网站
以此类推，网站目录可以存放在硬盘下的任何地方。
实现的过程如下：
1、打开apache的httpd.conf文件（有的时候是在etc/目录下），在Listen 80处另起一行输入Listen 8080 监听8080端口，如需其他端口需逐个添加：
<blockquote>Listen 80
Listen 1000
Listen 1001
Listen 1002
…</blockquote>
2.如果上边httpd.conf文件是在etc里找到的，那就在apache目录下的httpd.conf文件内添加一行
<blockquote>Include conf/extra/httpd-vhosts.conf   来设置启动虚拟机</blockquote>
如果在etc目录下的httpd.conf文件里找到这句代码，检查他前边是不是有#，有的话去掉就行了

3.在etc/extra/httpd-vhosts.conf   这个文件里添加以下代码
<blockquote>&lt;VirtualHost *:1003&gt;
DocumentRoot "/opt/lampp/htdocs/work2"
ServerName localhost                         用ServerAlias是子域名像什么www或者blog什么的 不是pengweb.net
&lt;/VirtualHost&gt;                                         上边这部分

&lt;Directory "/opt/lampp/htdocs/work2"&gt;
Options Indexes FollowSymLinks Includes ExecCGI
AllowOverride All
Order allow,deny
Allow from all
&lt;/Directory&gt;

NameVirtualHost *:80                             下边这个是必须添加的，这个我给删了 但是也没事
&lt;VirtualHost *:80&gt;
DocumentRoot "/opt/lampp/htdocs/"    这个是系统默认的存放网站文件的根目录
ServerName localhost
&lt;/VirtualHost&gt;</blockquote>
下边是网上搜集的，但是我有报错，所以只做修改参考，根据不同环境可能需要用到

在httpd.conf文件最后一行添加：
<blockquote>NameVirtualhost localhost:8080 # 虚拟主机端口            这里有的环境不用加，会报错
&lt;virtualhost localhost:8080&gt;
documentroot E:/sk  #这里就是你的网站目录绝对路径了哦~注意斜杠的方向
servername locahost:8080 #对应监听的端口
&lt;/virtualhost&gt;

&lt;Directory "E:/sk"&gt;
Options Indexes FollowSymLinks
AllowOverride All #允许URL重写
Order allow,deny
Allow from all
&lt;/Directory&gt;</blockquote>
完毕后记得重启apache，然后再浏览器输入<a href="http://localhost:8080/">http://localhost:8080/</a> 就可以访问到E:/sk下的网站了


<h3>数据库配置：</h3>


今天在学习使用chmod命令时候把/var/www以及子目录的权限改为了777，后来再打开就出现了以下错误：
<div>
<div><span style="color: #990030;">Wrong permissions on configuration file, should not be world writable!</span></div>
<div></div>
<div>后来在网上查了查，原来<span style="color: #9c5a3c;"><b>phpmyadmin必须在755权限</b></span>下才可以运行。</div>
<div></div>
<div>解决办法：</div>
<blockquote>
<div>cd /var/www</div>
<div>sudo chmod -R 755 phpmyadmin</div></blockquote>
<div></div>
<div>再访问，成功！</div>
<div></div>
<div>数据库在首页那选-----用户---然后添加用户----填用户名，密码，  然后创建一个数据库名</div>
<div></div>

<h3>安装Wordpress:</h3>

<div>在安装文档的根目录下<span style="color: #ff0000;"><strong>删除wp-config.php</strong></span>   然后直接访问网址就进入安装步骤了很简单。</div>
</div>