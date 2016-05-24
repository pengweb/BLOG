---
title: yum及apt常用命令
date: 2016-03-21 23:28:26
tags: [others,yum,linux]

---
# yum命令

因为Linux发行版比较之后，所以都用epel-release
``` bash
yum install epel-release
```

    yum check-update  检查可更新的所有软件包
    yum update  下载更新系统已安装的所有软件包
    yum upgrade  大规模的版本升级,与yum update不同的是,连旧的淘汰的包也升级
    yum install   安装新软件包
    yum update   更新指定的软件包
    yum remove   卸载指定的软件包
    yum groupinstall   安装指定软件组中的软件包
    yum groupupdate   更新指定软件组中的软件包
    yum groupremove   卸载指定软件组中的软件包
    yum grouplist  查看系统中已经安装的和可用的软件组
    yum list  列出资源库中所有可以安装或更新以及已经安装的rpm包
    yum list   列出资源库中与正则表达式匹配的可以安装或更新以及已经安装的rpm包
    yum list available  列出资源库中所有可以安装的rpm包
    yum list available   列出资源库中与正则表达式匹配的所有可以安装的rpm包
    yum list updates  列出资源库中所有可以更新的rpm包
    yum list updates   列出资源库中与正则表达式匹配的所有可以更新的rpm包
    yum list installed  列出资源库中所有已经安装的rpm包
    yum list installed   列出资源库中与正则表达式匹配的所有已经安装的rpm包
    yum list extras  列出已经安装的但是不包含在资源库中的rpm包
    yum list extras   列出与正则表达式匹配的已经安装的但是不包含在资源库中的rpm包
    yum list recent  列出最近被添加到资源库中的软件包
    yum search   检测所有可用的软件的名称、描述、概述和已列出的维护者，查找与正则表达式匹配的值
    yum provides   检测软件包中包含的文件以及软件提供的功能，查找与正则表达式匹配的值
    yum clean headers  清除缓存中的rpm头文件
    yum clean packages  清除缓存中rpm包文件
    yum clean all  清除缓存中的rpm头文件和包文件
    yum deplist   显示软件包的依赖信息
    当第一次使用yum 或yum 资源库有更新时，yum 会自动下载所有所需的he ade rs放置于 /var/cache /yum 目录下，所需时间可能较          长。
    还可以使用 yum info 命令列出包信息，yum info 可用的参数与 yum list 的相同。
    yum 命令还可以使用 -y 参数用于用 ye s 回答命令运行时所提出的问题，比如 yum -y install vsftpd，这样在安装软件的时候就不用输入yes/y了
    yum 命令工具使用举例
    1、升级系统
    [root@localhost ~]#yum update
    2、安装指定的软件包,我最喜欢用下面的命令
    [root@localhost ~]# yum -y install vsftpd
    3、升级指定的软件包
    [root@localhost ~]# yum -y update mysql
    4、卸载指定的软件包
    [root@localhost ~]# yum -y remore vsftpd mysql
    5、查看系统中已经安装的和可用的软件组，对于可用的软件组，你可以选择安装
    [root@localhost ~]# yum grouplist
    6、安装上一个命令中显示的可用的软件组中的一个软件组，神之编辑器-Emacs，大约安装了12个软件包
    [root@localhost ~]# yum -y groupinstall Emacs
    7、更新指定软件组中的软件包
    [root@localhost ~]# yum -y groupupdate Emacs
    8、卸载指定软件组中的软件包，对于Emacs，安装的时候安装了12个软件包，但是卸载的时候只卸载了4个软件包！
    [root@localhost ~]# yum -y groupremove Emacs
    9、清除缓存中的rpm 头文件和包文件
    [root@localhost ~]# yum clean all
    10、搜索相关的软件包
    [root@localhost ~]# yum -y search Emacs
    11、显示指定软件包的信息
    [root@localhost ~]# yum info Emacs
    和rpm -qi emacs显示的信息差不多，但不完全相同
    12、查询指定软件包的依赖信息，emacs依赖的模块不少啊
    [root@localhost ~]# yum deplist emacs
    13、列出所有以 yum 开头的软件包
    [root@localhost ~]# yum list yum\*
    14、列出已经安装的但是不包含在资源库中的rpm 包
    # yum list extras
    最常用的还是第3，4命令
    number of view: 225
    No related posts.
    启动动 yum 升级系统
    第一次执行yum check-update必须花比较久的时间，因為yum必须检查伺服器上所有header资料; 完成之后，往后执行 yum check-update就会很快了。
    在使用yum升级系统之前，基於系统安全性考量，yum需要所有RPM套件的GPG认证金钥，认证升级RPM套件的完整性之后，才能安全地帮您自动升级系 统，所以您必须先载入Fedora DVD安装光碟的RPM-GPG-KEY与RPM-GPG-KEY-fedora这两个GPG认证金钥档案，才能执行yum update自动升级所有RPM套件。
    # yum check-update　　　(检查需要升级的套件)
    # rpm --import RPM-GPG-KEY
    # rpm --import RPM-GPG-KEY-fedora
    # yum -y update 　　　(自动升级所有RPM套件)
    yum程式已经自动在系统的 /etc/cron.daily 目录中放有yum.cron，每天会定时帮您自动执行yum系统升级程式，自动检查并更新伺服器上update的新RPM套件，所有的yum执行过程也都 会记录在 /var/log/yum.log中，我们只要确定 cron、yum 的 service 有啟动，即会每天作 yum update 的动作了
    #chkconfig crond on
    #chkconfig yum on
    yum相关的套件
    Yum Extender
    是一套图形介面的yum更新程式，安装后会出现在 Xwindow的应用程式/系统工具/yum延伸程式。
    yum -y install yumex
    Yum UpdateOnBoot
    若电脑并非24小时开机，不适合作cron定时更新的主机，可设定在开机时检查是否有要更新的套件。
    yum -y install yum-updateonboot
    chkconfig yum-updateonboot on
    yum的常用指令
    更新套件
    yum update [套件1] [套件2] [...]  yum update
    安装套件
    yum install 套件1 [套件2] [...]
    yum install php*
    移除套件
    yum remove 套件1 [套件2] [...]  yum removel nmap
    列出所有的套件
    yum list
    列出所有可以更新的套件  yum list updates
    列出所有已安装的套件  yum list installed
    列出所有已安装但不在 Yum Repository 内的套件  yum list extras
    检查可以更新的套件  yum check-update
    列出所有套件的资讯  yum info
    列出所有可以更新的套件资讯  yum info updates
    列出所有已安装的套件资讯  yum info installed
    列出所有已安装但不在 Yum Repository 内的套件资讯  yum info extras
    列出套件提供哪些档案
    yum provides 套件1 [套件2] [...]
    搜寻套件
    yum search [参数]
    
# apt命令

`apt-get` 是一个下载安装软件包的简单命令行接口。 最常用的命令是update(更新) 和install(安装)。

**命令：**

update - 重新获取软件包列表 

upgrade - 进行更新 

install - 安装新的软件包 

remove - 移除软件包 

autoremove - 自动移除全部不使用的软件包 

purge - 移除软件包和配置文件 

source - 下载源码档案 

build-dep - 为源码包配置编译依赖 

dist-upgrade - 发行版升级

dselect-upgrade - 依照 dselect 的选择更新 

clean - 清除下载的归档文件 

autoclean - 清除旧的的已下载的归档文件 

check - 检验是否有损坏的依赖 

**选项：** 

-h 本帮助文件。 

-q 输出到日志 - 无进展指示 

-qq 不输出信息，错误除外 

-d 仅下载 - 不安装或解压归档文件 

-s 不实际安装。模拟执行命令

-y 假定对所有的询问选是，不提示 

-f 尝试修正系统依赖损坏处 

-m 如果归档无法定位，尝试继续

-u 同时显示更新软件包的列表 

-b 获取源码包后编译 -V 显示详细的版本号

-c=? 阅读此配置文件

-o=? 设置自定的配置选项，如 -o dir::cache=/tmp

**常用:**

apt-cache search packagename 搜索包
apt-cache show packagename 获取包的相关信息，如说明、大小、版本等
apt-get install packagename 安装包
apt-get install packagename --reinstall 重新安装包
apt-get -f install 修复安装”-f = –fix-missing”
apt-get remove packagename 删除包
apt-get remove packagename --purge 删除包，包括删除配置文件等
apt-get update 更新源
apt-get upgrade 更新已安装的包
apt-get dist-upgrade 升级系统
apt-get dselect-upgrade 使用 dselect 升级
apt-cache depends packagename 了解使用依赖
apt-cache rdepends packagename 是查看该包被哪些包依赖
apt-get build-dep packagename 安装相关的编译环境
apt-get source packagename 下载该包的源代码
apt-get clean 清理无用的包
apt-get autoclean 清理无用的包
apt-get check 检查是否有损坏的依赖