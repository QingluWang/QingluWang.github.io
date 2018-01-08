---
layout	:	post
title	:	配置HTTPS
---

## 概述

HTTPS就是在HTTP协议的基础上加入了SSL层，使得客户端与服务端之间通信更加安全

##	条件

<blockquote>
.crt文件<br>
.key文件
</blockquote>

## 过程

### 1.申请证书和密钥

申请SSL证书一般需要收费，当然也有免费的，可以去startssl.com申请

#### 1.域名认证


一般它会发一封带着verification code的邮件到你指定的邮箱里，填好该verification code即可

#### 2.提交CSR并获取证书

这里我用它的startcomtool.exe来生成CSR

点击Generate CSR，选择一个位置保存生成的.csr文件和.key文件(例如，temp.csr和temp.key)

之后copy CSR content的内容至submit CSR的文本框中

点击here下载一个压缩包文件

因为我用apache做web服务器，所以只需要提取ApacheServer里的域名.crt文件(例如temp.crt)

### 2.部署证书

上传前面的两个文件temp.key和temp.crt至一个指定目录(例如/temp)

在此以Apache2.4.23版本为例
<blockquote>
1、安装mod-ssl openssl<br><br>

2、修改apache目录下conf/extra/httpd-ssl.conf文件<br><br>

ServerName 你的域名<br>
SSLCertificateFile “/temp/temp.crt”<br>
SSLCertificateKeyFile “/temp/temp.key”<br>
	
&lt;Directory 网站路径&gt;<br>
AllowOverride All<br>
Require all granted<br>
SSLOptions +StdEnvVars<br>
&lt;/Directory&gt;<br><br>

3、修改apache目录下conf/httpd.conf文件<br><br>

LoadModule ssl_module modules/mod_ssl.so<br>
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so<br>
Include conf/extra/httpd-ssl.conf<br><br>

4、重启apache生效<br>
service httpd restart
</blockquote>