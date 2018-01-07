---
layout	:	post
title	:	Centos7下修改主机名
---
## 环境
>Centos7

## 主机名
输入`hostname`命令，就会显示当前主机的主机名.

在Centos中，有三种定义的主机名:
<blockquote>
1.静态的（static）<br>
“静态”主机名也称为内核主机名，是系统在启动时从/etc/hostname自动初始化的主机名。<br>
2.瞬态的（transient）<br>
“瞬态”主机名是在系统运行时临时分配的主机名，例如，通过DHCP或mDNS服务器分配。<br>
3.灵活的（pretty）
“灵活”主机名则允许使用自由形式（包括特殊/空白字符）的主机名，以展示给终端用户（如Linux）。
</blockquote>

*静态主机名和瞬态主机名都遵从作为互联网域名同样的字符限制规则。*

## 操作主机名
在Centos6下，只修改*/etc/sysconfig/network*文件即可，但是对于Centos7不可以。
在Centos7中，有个叫*hostnamectl*的命令行工具，它允许你查看或修改与主机名相关的配置。
>查看静态主机名<br>
>`hostnamectl -static`<br>
>查看瞬态主机名<br>
>`hostnamectl -transient`<br>
>查看灵活主机名<br>
>`hostnamectl -pretty`

要同时修改所有三个主机名：静态、瞬态和灵活主机名：

`hostnamectl set-hostname xxx`

一旦修改了静态主机名，*/etc/hostname* 将被自动更新。然而，*/etc/hosts*不会更新以保存所做的修改，所以你每次在修改主机名后一定要手动更新*/etc/hosts*，之后再重启Centos7。否则系统再启动时会很慢。