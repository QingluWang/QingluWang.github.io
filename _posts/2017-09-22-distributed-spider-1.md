---
layout	:	post
title	:	分布式爬虫（一）--环境搭建
---
## 环境

<blockquote>
Centos7<br>
Python 2.7.5<br>
Scrapy 1.4.0<br>
scrapy-redis 0.6.8<br>
</blockquote>

## 步骤：

### 1.安装python

`yum install python`<br>
*(yum list python 查看可供选择的版本)*

### 2.安装Scrapy

`pip install Scrapy`<br>
*(pip search Scrapy | grep Scrapy 找到并查看Scrapy版本)*

### 3.安装scrapy-redis

`pip install scrapy-redis`

参考网站：

Scrapy安装：<https://scrapy-chs.readthedocs.io/zh_CN/0.24/intro/install.html>

scrapy-redis安装：<https://github.com/younghz/scrapy-redis>