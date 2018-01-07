---
layout	:	post
title	:	wordpress安装
---
## 1、优点
快速、方便、可定制化高

## 2、条件
<blockquote>
1.php5.2.4或更新版本<br>
2.mysql5.0或更新版本<br>
3.云服务器<br>
4.wordpress压缩包<br>
5.apache或nginx(本文以apache为例)
</blockquote>

## 3、安装
>1.wordpress压缩包解压后放至apache默认网站目录下，具体可看httpd.conf,一般是xxx/www/html<br>
>2.将wordpress文件夹权限交给apache用户,
	`chown -r apache:apache xxx/wordpress`<br>
>3.用mysql新建数据库myblog<br>
>4.通过浏览器访问 x.x.x.x/wordpress进入安装界面,
>x.x.x.x是你的云服务器公网ip地址<br>
>5.配置相应信息，选数据库什么的

至此，wordpress搭建的blog网站就搭建好了。
