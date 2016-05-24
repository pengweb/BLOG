---
title: Centos/Ubuntu+Nodejs/Xampp服务器环境搭建
date: 2016-03-21 22:11:49
tags: [centos,linux,nodejs,xampp,服务器]

---
# Linux配置:

## 首先配置虚拟机-重要

编辑-虚拟网络编辑器-修改vmnet0为桥接模式
虚拟机-设置-网络适配器-修改为桥接模式

## 配置Linux文件
cd ..   先返回根目录
cd etc/sysconfig/network-scripts
vi ifcfg-eno*    修改这个文件*是不同Linux版本这个尾号不同，自己查
vi操作：
i 进入编辑界面
:wq! 保存退出
:q!  不保存退出

将内容改为如图下
![](/images/11111.jpg)
里边很多配置可以不用，可以自行百度

修改域名服务器-避免ping不通网址
cd etc/resolv.conf
添加下边这个
```bash
nameserver 8.8.8.8
nameserver 8.8.4.4
```

安装epel-因为Linux自己的yum发行版不全，所以通过这个扩展
```bash
yum install epel-release
```



## 安装NodeJS:

```bash
yum install nodejs
```

# Ubuntu配置
## 查看Ubuntu版本
```bash
uname -r
uname -a
lsb_release -a
cat /proc/version
```
## 更新系统及软件
```bash
sudo apt-get update        //更新系统资源
sudo apt-get upgrade            //升级检测，如果有可以升级的就可以进行升级
sudo apt-get upgrade  软件资源名 //升级单个软件到最新版本
sudo apt-get dist-upgrade       //升级所有软件到最新版本
```

## 安装curl包管理工具和Nodejs
```bash
apt-get update  //一定要先更新，否则很多都找不到
apt-get install curl
apt-get install nodejs   //直接用apt-get就可以了，不用curl也可以

//下边是另外一个人的
apt-get update  
apt-get install -y python-software-properties software-properties-common  
add-apt-repository ppa:chris-lea/node.js  
apt-get update  
apt-get install nodejs  
```

# 安装Xampp:

```bash
cd /home
cd /zhp
cd Desktop
chmod a+x xampp```````.run
sh 文件名-这个不能执行-直接输入文件名也不能执行
./文件名 执行安装
ls当前文件夹
su - 获取权限
cd -返回上一级目录
```
每次执行：
```
cd /opt
cd lampp
sudo ./manager-linux-x64.run
```



# 配置子目录多站点:


经常需要在本地调试网站，却又不喜欢在<a href="http://localhost/">http://localhost/</a>网站的文件夹名，且几个比较重要的项目我想直接用端口号以示区分，想达到的效果如下：
<a href="http://localhost/">http://localhost/</a>     默认80端口的时候访问的是D:\目录下的A网站
<a href="http://localhost:8080/">http://localhost:8080/</a>    8080端口的时候访问的是E:\目录下的B网站
以此类推，网站目录可以存放在硬盘下的任何地方。
实现的过程如下：
1、打开apache的httpd.conf文件（有的时候是在etc/目录下），在Listen 80处另起一行输入Listen 8080 监听8080端口，如需其他端口需逐个添加：
```bash
Listen 80
Listen 1000
Listen 1001
Listen 1002
…
```
2.如果上边httpd.conf文件是在etc里找到的，那就在apache目录下的httpd.conf文件内添加一行
```bash
Include conf/extra/httpd-vhosts.conf   //来设置启动虚拟机
```
如果在etc目录下的httpd.conf文件里找到这句代码，检查他前边是不是有#，有的话去掉就行了

3.在etc/extra/httpd-vhosts.conf   这个文件里添加以下代码
```bash
<VirtualHost *:1003>
DocumentRoot "/opt/lampp/htdocs/work2"
ServerName localhost                         用ServerAlias是子域名像什么www或者blog什么的 不是pengweb.net
</VirtualHost>                                         上边这部分

<Directory "/opt/lampp/htdocs/work2">
Options Indexes FollowSymLinks Includes ExecCGI
AllowOverride All
Order allow,deny
Allow from all
</Directory>

NameVirtualHost *:80                             下边这个是必须添加的，这个我给删了 但是也没事
<VirtualHost *:80>
DocumentRoot "/opt/lampp/htdocs/"    这个是系统默认的存放网站文件的根目录
ServerName localhost
</VirtualHost>
```
下边是网上搜集的，但是我有报错，所以只做修改参考，根据不同环境可能需要用到

在httpd.conf文件最后一行添加：
```bash
NameVirtualhost localhost:8080 # 虚拟主机端口            这里有的环境不用加，会报错
<virtualhost localhost:8080>
documentroot E:/sk  #这里就是你的网站目录绝对路径了哦~注意斜杠的方向
servername locahost:8080 #对应监听的端口
</virtualhost>

<Directory "E:/sk">
Options Indexes FollowSymLinks
AllowOverride All #允许URL重写
Order allow,deny
Allow from all
</Directory>
```
完毕后记得重启apache，然后再浏览器输入<a href="http://localhost:8080/">http://localhost:8080/</a> 就可以访问到E:/sk下的网站了


# 数据库配置：


今天在学习使用chmod命令时候把/var/www以及子目录的权限改为了777，后来再打开就出现了以下错误：
Wrong permissions on configuration file, should not be world writable!
后来在网上查了查，原来**phpmyadmin必须在755权限**下才可以运行。
解决办法：
```bash
cd /var/www
sudo chmod -R 755 phpmyadmin
```

再访问，成功！
数据库在首页那选-----用户---然后添加用户----填用户名，密码，  然后创建一个数据库名


# 安装Wordpress:

在安装文档的根目录下**删除wp-config.php**然后直接访问网址就进入安装步骤了很简单。