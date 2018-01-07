---
layout	:	post
title	:	Linux网络配置
---
## 环境
>Centos7

##	概述
在Linux环境下，进行网络配置有4种方式:

<blockquote>	
1.ifconfig命令临时配置网络<br>

2.setup界面配置网络<br>

3.修改网络配置文件<br>

4.图形界面配置网络<br>
</blockquote>
 
## 详情
### 1.ifconfig命令临时配置网络

举个例子，除本地网卡lo外，还有一块网卡eth0

临时配置ip地址和子网掩码：

`ifconfig eth0 192.168.1.103 netmask 255.255.255.0`

### 2.setup界面配置网络

setup这个工具，红帽专有，Debian系貌似无法使用

运行命令setup就会进入setup界面配置网络


如果是Centos最小化安装，那么是没有setup的，需要自己进行安装

`yum -y install setuptoo`

`yum  install ntsysv`

`yum install iptables`

`yum install system-config-network-tui`

`yum install system-config-securitylevel-tui`

`setup`

### 3.修改网络配置文件

#### 1.网卡信息文件

`vi /etc/sysconfig/network-scripts/ifcfg-eth0`

<blockquote>
TYPE:一般是以太网，即Ethernet<br><br>
BOOTPROTO:指定方式来获取ip地址，此处有三种：static、none、dhcp<br><br>

static和none是手动分配ip，dhcp是自动分配ip,前提是局域网内有dhcp服务器
</blockquote>

*DHCP–动态主机配置协议，给内部网络或网络服务供应商自动分配ip地址*

*ONBOOT:表示网卡etho会不会随网络服务的启动而启动*

*用setup配置完网络之后，记得修改此文件，把ONBOOT=no改为ONBOOT=yes*

#### 2.主机名文件
<blockquote>
Centos7里是用hostnametl这个工具和/etc/hosts进行主机名更改

Centos6里是更改/etc/sysconfig/network
</blockquote>
#### 3.配置DNS

`vi /etc/reslov.conf`

*将nameserver–域名服务器ip修改*

### 4.图形界面配置网络

在Linux图形界面下，配置网络其实跟在win操作系统下差不多