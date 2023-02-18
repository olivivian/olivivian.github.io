---
title: Docker安装Jenkins保姆级教程
date: 2023-01-06
categories: 工具
summary: 从Docker到Jenkins的安装步骤
img: https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/hexo/14.jpg
tags:
  - Docker
  - Jenkins
---

# Docker安装

查看当前系统内核版本，docker要求是高于3.10

```
uname -r
```

更新yum包到最新，yum是Linux比较常用到的命令功能,是一个Shell前端软件包管理器。

```
sudo yum update
```

安装需要的软件包 yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的

```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

设置yum源

```
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

可以查看所有仓库中所有docker版本，并选择特定版本安装

```
yum list docker-ce --showduplicates | sort -r
```

安装docker 

```
sudo yum install docker-ce  
```

启动并加入开机启动

```
sudo systemctl start docker
sudo systemctl enable docker
```

验证安装docker是否成功

```
docker version
```

# Jenkins安装

创建映射目录，可以在var目录下创建

```
# 在适当的位置创建映射目录
mkdir -p jenkins_home
# 查看目录权限
ls -nd jenkins_home
# 改变拥有者为管理员（如果没有权限，会导致映射失败）
sudo chown -R 1000:1000 jenkins_home
```

在docker中安装jenkins

```
# 创建一个新的容器并运行一个命令
docker run -d --name jenkins -p 8080:8080  -v /var/jenkins_home:/var/jenkins_home jenkinsci/blueocean
```

> **-d:** 后台运行容器，并返回容器ID
>
>  **-p 8080:8080**:将镜像的8080端口映射到服务器的8080端口
>
> **--name="nginx-lb":** 为容器指定一个名称，如果没有指定，会自动生成一个随机名称
>
>  **-v /var/jenkins_home:/var/jenkins_home** ：主机的目录映射到容器的目录；
>
> **jenkinsci/blueocean**：IMAGE名称

安装成功，这边这一串是登录密码

![image-20230105175136022](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230105175136022.png)

通过主机ip:8080，登录jenkins，如果登录成功，把上面的密码复制过来

![image-20230105192625279](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230105192625279.png)



解锁Jenkins后，安装推荐的插件，配置用户名密码，重启Jenkins，登录即可。

![image-20230106115919561](C:/Users/Axjy/AppData/Roaming/Typora/typora-user-images/image-20230106115919561.png)

# 问题

如果进入失败，检查容器是否正确开启，端口映射是否正确

```
docker ps -a  //查看所有容器
```

![image-20230106114014951](https://imgstorage-1313684358.cos.ap-nanjing.myqcloud.com/img/image-20230106114014951.png)

```
查看端口号是否开放，命令：netstat -natp
```

```
查看Jenkins进程是否还在，命令 ps -ef|grep jenkins
```

```
查看服务器的安全组规则Jenkins端口号，是否开放（我们这需要检查的端口是8080）
腾讯云轻量服务器开放端口方法教程：https://zhuanlan.zhihu.com/p/411605768
```

> [jenkins无法访问](https://blog.csdn.net/weixin_44909045/article/details/123329216)
>
> [v挂载目录导致的容器启动失败](https://blog.csdn.net/qq_41615959/article/details/121053604)

