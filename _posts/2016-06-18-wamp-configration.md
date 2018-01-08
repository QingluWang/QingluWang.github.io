---
layout	:	post
title	:	wamp多站点配置
---
## 环境

>windows<br>
>wampserver

## 过程

### 1.仅改动apache默认站点路径
在【wamp路径】\bin\apache\apachex.x.x\conf里找到apache配置文件–httpd.conf,寻找documentroot
DocumentRoot “改为需要运行的网站路径”

*不要在网站路径里出现中文！*
### 2.配置单个站点或多个站点
#### 1.单个站点
1.在【wamp路径\wamp\bin\apache\apachex.x.x\conf\extra里找到httpd-vhosts.conf添加
<blockquote>
DocumentRoot “改为需要运行的网站路径”<br>
ServerName 主机名,在网址栏中输入可以直接访问
</blockquote>
2.在【wamp路径】\bin\apache\apachex.x.x\conf里找到apache配置文件–httpd.conf,寻找onlineoffline，改为如下
<blockquote>
Order Deny,Allow<br>
Allow from all<br>
Require all granted
</blockquote>
3.在【wamp路径】\bin\apache\apachex.x.x\conf里找到apache配置文件–httpd.conf,寻找httpd-vhosts.conf，添加

*Include conf/extra/httpd-vhosts.conf*

4.在C:\Windows\System32\drivers\etc中找到HOSTS文件，编辑最后面添加

*127.0.0.1 想要在网址栏中直接访问的主机名*
#### 2.多个站点
跟单个站点差不多，只是第一步和最后一步里添加相应站点信息。

*可能会出现You don’t have permission to access / on this server*

*解决方法:*

*把localhost作为一个”站点”添加。*