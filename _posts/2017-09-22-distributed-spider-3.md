---
layout	:	post
title	:	分布式爬虫（三）--Mariadb安装及配置
---

## 安装

`yum install mariadb mariadb-server`

## 配置

### 1.启动Mariadb：

`systemctl start mariadb`

### 2.设置开机启动：

`systemctl enable mariadb`

### 3.简单配置：

`mysql__secure__installation`

跟着一步一步走下去，结束

### 4.配置MariaDB的字符集：

文件/etc/my.cnf<br>
`vim /etc/my.cnf`<br>
在[mysqld]标签下添加
<blockquote>
init_connect='SET collation_connection = utf8_unicode_ci'<br>
init_connect='SET NAMES utf8'<br>
character-set-server=utf8<br>
collation-server=utf8_unicode_ci<br>
skip-character-set-client-handshake
</blockquote>

文件/etc/my.cnf.d/client.cnf<br>
`vim /etc/my.cnf.d/client.cnf`<br>
在[client]中添加
>default-character-set=utf8

文件/etc/my.cnf.d/mysql-clients.cnf

`vim /etc/my.cnf.d/mysql-clients.cnf`<br>
在[mysql]中添加
>default-character-set=utf8

全部配置完成，重启mariadb<br>
`systemctl restart mariadb`<br>
之后进入MariaDB查看字符集
<blockquote>
mysql> show variables like "%character%";<br>
mysql> show variables like "%collation%";
</blockquote>

## 添加用户

### 1.进入mariadb：

`mysql -uroot -p`

### 2.创建spider用户：

`create user spider@localhost identified by 'spider';`

### 3.创建spider数据库：

`create database spider;`

### 4.分配权限：

`grant all privileges on spider.* to spider@'%' identified by 'spider';`