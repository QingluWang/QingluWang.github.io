---
layout: post
title: RaspberryPi制作无线路由器
---
## 环境

<blockquote>
树莓派<br>
USB无线网卡<br>
网线<br>
超级终端（XShell、Putty等）
</blockquote>

## 过程

### 1.配置网络环境:

#### 1.准备工作

用一条网线联通树莓派和电脑，电脑连接可上网的无线，开启共享，之后在cmd里输入arp –a,找到一个与本机同网段的IP，例如192.168.137.22,设置电脑以太网固定IP跟它是同一网段，比如设为192.168.137.66，用Xshell访问192.168.137.22，输入树莓派给的用户名和密码，进入raspbian.

#### 2.安装hotspot(hostapd)

`sudo apt-get install bridge-utils hostapd`

#### 3.安装udhcp

`sudo apt-get install udhcpd`

*udhcpd是为连接到热点的设备分配IP地址的一个服务，遵从DHCP协议*

#### 4.配置udhcpd.conf文件

`sudo vim /etc/udhcpd.conf`
<blockquote>
wifi热点分配的ip地址范围，start–>end

udhcp服务的接口，设为wlan0网卡接口

配置dns(opt dns)、子网掩码(opt subnet)、路由地址(opt router)、十天内DHCP以秒为单位的租约时间(opt lease 86400)
</blockquote>

#### 5.配置无线网卡部分信息

`sudo vim  /etc/network/interfaces`

允许一个无线网卡wlan0热插拔，即*allow-hotplug  wlan0*,然后把无线网卡的IP地址设为静态且固定的。

#### 6.配置hostapd.conf文件

`sudo vim /etc/hostapd/hostapd.conf`

<blockquote>
ssid–wifi	热点名称<br><br>
wpa_passphrasse	wifi热点密码<br><br>
channel	一般3 9 11信号比较好<br>
</blockquote> 

#### 7.开通NAT

`sudo sh –c “echo 1 > /proc/sys/net/ipv4/ip_forward”`

`vim /etc/sysctl.conf`

*改动此行为net.ipv4.ip_forward=1*

#### 8.配置iptables防火墙

`sudo iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE`

`sudo iptables –A FORWARD –i eth0 –o wlan0 –m state –state RELATED,ESTABLISHED –j ACCEPT`

`sudo iptables –A FORWARD –i wlan0 –o eth0 –j ACCEPT`

将刚才配置的iptables保存下来以便下次使用

`sudo sh –c “iptables-save > /etc/iptables.ipv4.nat”`

`sudo vim /etc/network/interfaces`

在最后加上

*up iptables-restore < /etc/iptables.ipv4.nat*

#### 9.重启并测试

`sudo reboot`

`sudo hostapd –dd /etc/hostapd/hostapd.conf`

若无错误，则能搜到你自己配的无线信号了

Ctrl+C退出测试

#### 10.设置hostapd的配置文件路径

`sudo vim /etc/default/hostapd`

去掉注释符号并改动下面这行，为我们的配置文件路径

*DAEMON_CONF=”/etc/hostapd/hostapd.conf”*

#### 11.启动相应软件和加入启动项

`sudo service hostapd start`

`sudo service udhcpd start`

`sudo update-rc.d hostapd enable`

`sudo update-rc.d udhcpd enable`

*若无线网卡配置的DHCP不能发挥作用，ifconfig –a 后，发现wlan0的ip地址并不是我们指定的静态IP地址*

*解决办法：*

`sudo vim /etc/default/ifplugd`

加入如下内容

*INTERFACES=”eth0″ HOTPLUG_INTERFACES=”eth0″ ARGS=”-q -f -u0 -d10 -w -I” SUSPEND_ACTION=”stop”*

原文链接:<http://wangye.org/blog/archives/845/>

