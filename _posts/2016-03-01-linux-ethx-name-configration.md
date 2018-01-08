---
layout	:	post
title	:	Centos7网卡eth167777xx改回eth0
---

## 1.改网卡配置文件名

`cd /etc/sysconfig/network-scripts/`<br>

`mv ifcfg-eth167777xx ifcfg-eth0`

## 2.修改网卡配置文件信息[NAME参数]

`vi ifcfg-eth0`

找到NAME=eth167777xx<br>

改为NAME=eth0

## 3.修改grub文件来禁用内核继续使用该命名规则

`cd /etc/sysconfig`<br>

`vi grub`<br>

在”GRUB_CMDLINE_LINUX“变量中添加一句”net.ifnames=0 biosdevname=0“.

## 4.重新生成grub配置并更新内核参数

`grub2-mkconfig -o /boot/grub2/grub.cfg`