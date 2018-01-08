---
layout	:	post
title	:	Linux内存申请
---

## 环境

>Centos7

## 相关文件
>/proc/meminfo,/proc/sys/vm/overcommit_memory

## 内容：

为了避免超出内存的情况经常发生，Linux对于进程申请内存有一套机制，即对于内存使用超出某一阈值后再申请内存的处理方法–memory overcommit处理机制。

Linux对于overcommit有如下三种处理机制



简单概括就是：
<blockquote>
0–允许试探性的内存申请，但拒绝太大的内存申请(系统默认的模式)<br>
1–允许overcommit，尽情申请内存<br>
2–禁止overcommit(达到某一阈值)<br>
</blockquote>

相关内容
<blockquote>
1.本机模式：查看 /proc/sys/vm/overcommit_memory<br>
2.对于模式2，查看 /proc/meminfo,
获得CommitLimit值，超过此值即禁止内存申请<br>
3.设置overcommit处理模式：<br>
sysctl vm.overcommit_memory=x
</blockquote>
 

参考资料：<https://www.kernel.org/doc/Documentation/vm/overcommit-accounting>