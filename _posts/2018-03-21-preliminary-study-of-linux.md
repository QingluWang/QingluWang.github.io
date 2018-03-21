---
layout	:	post
title	:	初探Linux(九)--进程
---

##概述

？进程与程序的区别<br>
程序是存放在存储介质中的文件，进程是程序运行的实例。<br>
？进程的分类<br>
僵尸进程、孤儿进程、守护进程。<br>
？进程的生命周期<br>
等待态、就绪态、运行态。<br>
？Linux如何管理进程<br>
Linux通过PCB记录及管理进程。

##详情

###1.生命周期

等待态：<br>
&nbsp;&nbsp;进程因不具备某些执行条件而暂时无法继续执行的状态。<br>
就绪态：<br>
&nbsp;&nbsp;进程已经具备执行的一切条件，正在等待分配CPU的处理时间。<br>
运行态：<br>
&nbsp;&nbsp;该进程正在占用CPU运行。<br>
	
###2.分类

僵尸进程：<br>
&nbsp;&nbsp;子进程退出，父进程未执行wait系统调用，导致子进程资源未被释放，pid依旧存在进程表中。<br>
孤儿进程：<br>
&nbsp;&nbsp;子进程未执行完毕，父进程退出。<br>
守护进程：<br>
&nbsp;&nbsp;在后台运行的特殊进程。<br>
	
###3.控制

####(1)PCB--Process Control Block

作用:<br>
&nbsp;&nbsp;描述进程的当前情况以及控制进程运行的全部信息,是一种记录性的数据结构。<br>
位置：<br>
&nbsp;&nbsp;linux源代码/linux/include/linux/sched.h中的task_struct结构体。<br>

####(2)系统调用及库函数

获取进程号：<br>
&nbsp;&nbsp;pid\_t getpid()、pid\_t getppid()、pid\_t getpgid()<br>
头文件：sys/types.h、unistd.h<br>
创建进程：<br>
&nbsp;&nbsp;pid\_t fork(void)<br>
头文件：sys/types.h、unistd.h<br>
挂起进程：<br>
&nbsp;&nbsp;unsigned int sleep(unsigned int sec)、pid_t wait(int \*status)、pid\_t waitpid(pid\_t pid, int \*status,int options)<br>
头文件：unistd.h、sys/types.h、sys/wait.h<br>
结束进程：<br>
&nbsp;&nbsp;void exit(int value)、void _exit(int value)<br>
头文件：unistd.h