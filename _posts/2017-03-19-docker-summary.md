---
layout	:	post
title	:	浅谈docker
---

## Docker定义

Docker官网给了定义–Docker is the world’s leading software container platform.所以，docker就是一个软件容器平台。

## Docker优势
<blockquote>
1、快速部署<br>

2、提高服务器资源利用效率<br>

3、降低运维成本<br>
</blockquote>
## Docker原理

Docker的隔离技术源自LXC，即Linux Container，是Linux内核虚拟化技术，而LXC与cgroup是密不可分的，cgroup–control group是Linux内核用来控制进程组的资源框架，它可以按照用户自定义的群组对系统运行的进程进行区分，即一个docker,一个group。

Docker主要基于LXC,NameSpace,Cgroup,UnionFs等技术实现。

## Docker与虚拟机的比较

虚拟机如VmWareWorkStation,采用的是硬件辅助虚拟化技术。

在HostOS宿主机的层面上，Hypervisor构建出一套完整的虚拟硬件系统，在此之上再构建GuestOS虚拟机，即运行在本地OS上的OS,在此之上再运行一系列基于GuestOS的软件。

Docker采用的是操作系统级虚拟化技术，内核通过虚拟多个操作系统实例来隔离多个不同的进程,因此docker与宿主机共享kernel。

Docker省去了Hypervisor这一层，取而代之的是DockerEngine,在HostOS基础上直接进行资源调度，分配资源给各个进程。

## Docker基本用法

此处以Centos7.2为例进行说明

### 1.安装docker

`yum install -y docker`

### 2.配置DaoCloud镜像加速(docker初始镜像源在国外，国内访问比较慢)

<https://www.daocloud.io/>

登录进控制台找加速器即可

### 3.拉取images(此处以apache为例)

`docker pull httpd`

### 4.运行container

`docker run -d httpd`

### 5.查看container状态

`docker ps`

## 构建Docker镜像(构建自己需要的镜像)

通过dockerfile文件构建单个镜像

dockerfile文件是一个脚本文件,通过它来构建单个镜像

此处以构建简单apache镜像为例,文件名Dockerfile
<blockquote>
FROM–此后的各项操作基于哪个基础镜像<br>

MAINTAINER–作者<br>

RUN–镜像构建过程中执行<br>

CMD–用镜像构建容器后执行<br>
</blockquote>
`docker build -t test .`

`docker images`可以查看到刚刚构建的镜像

## 常用网站

Docker官网 : <https://www.docker.com>

DaoCloud加速器 : <https://www.daocloud.io/>

Docker镜像市场: <https://hub.docker.com/>