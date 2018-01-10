---
layout	:	post
title	:	树莓派开机自动连接wifi
---

## 文件

>/etc/wpa_supplicant/wpa_supplicant.conf

## 修改

文件末尾追加

<blockquote>
network={ <br>
&nbsp;&nbsp;&nbsp;&nbsp;ssid="wifi名称"<br> 
&nbsp;&nbsp;&nbsp;&nbsp;psk="wifi密码"<br> 
} 
</blockquote>

然后重启树莓派