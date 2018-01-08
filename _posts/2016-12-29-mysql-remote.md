---
layout	:	post
title	:	Mysql开启远程连接
---
## 过程

### 1.进入mysql
`mysql -u 用户名 -p`

### 2.在mysql数据库里进行授权
`grant all privileges on *.* to ‘root’@’%’ identified by ‘设置该用户登录的密码’ with grant option;`

### 3.重载系统权限并退出
`flush privileges;`
`exit;`

### 4.配置防火墙规则
`vim /etc/sysconfig/iptables`

加入
*-A INPUT -p tcp -m tcp –dport 3306 -j ACCEPT*

### 5.重启防火墙查看端口开启状态
`service iptables restart`

`service iptables status`
### 6.使此配置重启后依然生效（只想临时生效可以跳过此步骤）
`service iptables save`
### 7.此时生产环境是不安全的，远程管理之后应该关闭端口，删除之前添加的规则
`vim /etc/sysconfig/iptables`


删除之前添加的3306端口的那一行并添加以下规则禁用3306端口


*-A INPUT -p tcp -m tcp –dport 3306 -j DROP*

原文链接：<http://www.codesec.net/Linux/2015-07/120581.htm>
