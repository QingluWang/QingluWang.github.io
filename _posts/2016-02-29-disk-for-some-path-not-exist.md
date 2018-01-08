---
layout	:	post
title	:	为某个目录比如说/home准备的磁盘尚未就绪或不存在
---

可以先用命令fdisk –l【查看磁盘分区状况】，也可无

先用命令lsblk【查看各sd相应挂载状况】

看看 /home挂载的是哪个sd,记住该sd,比如说是sda10

再用命令`ls -l /dev/disk/by-uuid`【查看各个sd的uuid】

记下sda10的uuid

最后用命令`sudo gedit /etc/fstab`【将sda10的错误的uuid改为之前记下的sda10的uuid】

*UUID–通用唯一识别码，*
*linux分区挂载里使用uuid的好处就是当分区顺序改变或者新增分区时，仍然能够保证系统挂载分区不会出现问题*