---
title: Docker--学习笔记
date: 2016-05-23 09:56:36
tags: [docker,others]

---

仓库→镜像(ubuntu)→容器(其实就是镜像的实例)

# 安装Docker
基于CentOS7系统安装
```bash
sudo yum install docker
```
# 查看Docker版本
```bash
docker version
```

# 运行Docker deamon
```bash
sudo service docker start
```

# 默认开机启动
```bash
sudo chkconfig docker on
```

# 下载镜像
```bash
sudo docker pull ubuntu
```

# 查看镜像是否存在
```bash
sudo docker images ubuntu
```

# 查看编译好的镜像
```bash
sudo docker images
```

# 查看正在运行的容器
```bash
sudo docker ps
sudo docker ps -l
sudo docker ps -a
```
更详细
```bash
sudo docker inspect efe   //efe是id的前三位
```

# 运行镜像-进入bash控制台
```bash
sudo docker run -i -t ubuntu /bin/bash
sudo docker run -i -t ubuntu /bin/echo hello  //错误
```
参数解释
-t:开启一个终端
-i:以交互模式运行
# 安装新程序(安装node)
```bash
docker run ubuntu apt-get install -y node
```
在执行apt-get 命令的时候，要带上-y参数。如果不指定-y参数的话，apt-get命令会进入交互模式，需要用户输入命令来进行确认，但在docker环境中是无法响应这种交互的。

# 保存修改
```bash
docker commit 698 pengweb/u-node //起个新名字
```

```bash
docker ps -l 
```
获得id，只取前3位698就够了

# 发布自己的镜像
```bash
docker login
docker push pengweb/u-node
```

# 删除镜像-必须停止所有的容器
```bash
//停止所有container
docker stop $(docker ps -a -q)
//删除所有container
docker rm $(docker ps -a -q)
//删除images，通过image的id来指定删除谁
docker rmi <image id>
//删除untagged images，也就是那些id为<None>的image的话可以用
docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
//要删除全部image的话
docker rmi $(docker images -q)
```

[参考文章1](http://www.docker.org.cn/book/docker/what-is-docker-16.html)
[参考文章2](http://cache.baiducontent.com/c?m=9d78d513d9951cfe01bad4690d67c0161943f7682ba7a4020fd28449e3732a4b501095ac56260770d6d27d175ffc020baae47132690c7af1dd8a9f4baea68f6d6acd3034074dda114c8e4ceedc4652907dcf47bef145bce6ad2fd1b3d3d9d45f50cb57127af7aacd055e&p=896dca0485cc43ff57ed9779610a8e&newp=8d769a4786cc41ac5fb6c320550a96231610db2151d4db166b82c825d7331b001c3bbfb423221a02d3c17d610aae4a5bedf43c74360421a3dda5c91d9fb4c57479&user=baidu&fm=sc&query=docker+%B2%E9%BF%B4%C8%DD%C6%F7layer&qid=c35423cc000495af&p1=2)