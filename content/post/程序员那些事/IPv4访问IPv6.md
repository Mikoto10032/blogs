---
date: 2018-06-29
title: "IPv4访问IPv6"
tags:
    - 计算机网络
    - 翻墙
    - IPv6
categories:
    - 程序员那些事
comment: true
---
## 法一：4to6隧道				

### 1.6plat.org+openVPN（多平台）			
* 方案优点：无需资金投入，部署迅速，可以访问国内ipv6站点和一部分国外被封锁的ipv6站点

* 缺点：
	* 1、vpn带宽有限，无法进行大批量的传输；
	* 2、无法通过wifi或者代理的方式进行分享；			

* 主流平台均支持：			
	* 官网：http://bbs2.6plat.org/d/19
	* 个人账号申请：http://bbs2.6plat.org/d/23
	* 使用手册：http://bbs2.6plat.org/d/19
* Linux配置客户端			
	* 安装OpenVPN		
	
	```
	apt-get install openvpn
	```		
	* 配置文件到 `/etc/openvpn/6plat.ovpn`		
		 ```
client
dev tun
proto tcp
remote 46.6plat.org 9185
comp-lzo
resolv-retry infinite
nobind
persist-key
persist-tun
setenv CLIENT_CERT 0
auth-user-pass
remote-cert-tls server
verb 3
sndbuf 0
rcvbuf 0
cipher none
<ca>
-----BEGIN CERTIFICATE-----
MIIE3zCCA8egAwIBAgIJAJVvrlqcS4YsMA0GCSqGSIb3DQEBCwUAMIGlMQswCQYD
VQQGEwJDTjEQMA4GA1UECBMHQmVpamluZzEQMA4GA1UEBxMHQmVpamluZzESMBAG
A1UEChMJNnBsYXQub3JnMRMwEQYDVQQLEwo2cGxhdGdyb3VwMRUwEwYDVQQDEww2
cGxhdC5vcmcgQ0ExEDAOBgNVBCkTB0Vhc3lSU0ExIDAeBgkqhkiG9w0BCQEWETZw
bGF0QGJpaWdyb3VwLmNuMB4XDTE3MDEwNDA5MTc1NVoXDTI3MDEwMjA5MTc1NVow
gaUxCzAJBgNVBAYTAkNOMRAwDgYDVQQIEwdCZWlqaW5nMRAwDgYDVQQHEwdCZWlq
aW5nMRIwEAYDVQQKEwk2cGxhdC5vcmcxEzARBgNVBAsTCjZwbGF0Z3JvdXAxFTAT
BgNVBAMTDDZwbGF0Lm9yZyBDQTEQMA4GA1UEKRMHRWFzeVJTQTEgMB4GCSqGSIb3
DQEJARYRNnBsYXRAYmlpZ3JvdXAuY24wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAw
ggEKAoIBAQDpTRpxYttg0EsUYWCE3GKLMPTDXlzVtn93yb9MdgUJkCiGNgaXHQ6Y
NCcOXb3pLIxZN7eYH873ZgAY74+LiEIIAAPn+CTQjTcZ82r92xuSj47mMNd4/CcG
5byC9clsNijsWvJ7Rq2Fy2ynSddWMMkmVGZ8oS3psPc57cEOBUBdhTI4szo6aLE0
N3/AAFpIdfxlTATc5EWFxEk4SMPWAIcqkvZ1ETBit+HHU+Bv2oYcpzzi6jHmVw0d
EofxV0w3AUNUN894mWprBtZKZ+DVqms0+LI3mLWPXsv3m8zYBNTXqgE5p4vJ+E3J
3AzDKH2Rb/coBiy3V2g0Cdgc9vATQ4XzAgMBAAGjggEOMIIBCjAdBgNVHQ4EFgQU
M/hZJqaKeV9UVH6WoS7iwAk8/Q0wgdoGA1UdIwSB0jCBz4AUM/hZJqaKeV9UVH6W
oS7iwAk8/Q2hgaukgagwgaUxCzAJBgNVBAYTAkNOMRAwDgYDVQQIEwdCZWlqaW5n
MRAwDgYDVQQHEwdCZWlqaW5nMRIwEAYDVQQKEwk2cGxhdC5vcmcxEzARBgNVBAsT
CjZwbGF0Z3JvdXAxFTATBgNVBAMTDDZwbGF0Lm9yZyBDQTEQMA4GA1UEKRMHRWFz
eVJTQTEgMB4GCSqGSIb3DQEJARYRNnBsYXRAYmlpZ3JvdXAuY26CCQCVb65anEuG
LDAMBgNVHRMEBTADAQH/MA0GCSqGSIb3DQEBCwUAA4IBAQBzYlX/RgvViVvcxwGQ
SN9wP32U9aALFI4GCQz6ODrlYVx4m00zJeuR69bjLO3NZgMv6LtcovbuME+FYq/4
uXJJIfMlo2S/kKp5dBaGk9ERx0xs2OLAKyzc4wgx5zah5Nke1NhdYdCB6Lj6tM+s
vthNz2SWpcctvlOvV+5IdVrefiaLl7RBgf2j81DYmPCILZwHo8rQ0zKppgqAFcFk
tDO0FnHQcwe6xfTE1cIoOU39t+hTnvxQDBW4p9xkxX0hAFnNV41OadgEwxqyo6J0
BZ4dtEw8E9FFF8ewWl897xSv6AMPZTizFl3OReE376Kgv+gtFlSuj4kizCd7uiRp
o5ab
-----END CERTIFICATE-----
</ca>
 
			```			
	* 配置文件到`/etc/openvpn/client.ovpn`

PS:其他类似的软件还有[六飞](http://www.6fei.com.cn/)、[veno	](http://www.veno2.com/)		

### 2.miredo（Linux only）		
* 安装		

```
sudo apt-get install miredo
```
* 检测			
看到 teredo 这个虚拟网卡就可以用它访问 ipv6 了

```
ifconfig
```
* 用隧道客户端软件miredo来访问IPv6,但我发现，系统总是优先使用IPv4而不是IPv6.测试方法： http://www.kame.net/ 乌龟是活动的 说明是通过IPv6访问，否则就是通过IPv4访问的。

### 3.gw6c(gateway6 client)		
* 安装(安装后可能要重启机器。)			

```
  sudo apt-get install gw6c
```
* 修改防火墙IPv6设置 		

```
  sudo gedit /etc/default/ufw
```
找到**IPV6=no** 改为**IPV6=yes**			
* 测试http://www.kame.net/  终于发现乌龟动起来了。

*  PS: 刚安装好gw6c后，系统需要10多分钟才能连接服务器成功，请耐心等待。多半就能自己配置成功。如果发现现gw6c有时无法开机启动，有时又可以，各种开机启动的方法都试过了，但还是不行，不知为何？ 没有办法如果发现没有启动，则要手工启动之： sudo gw6c start 并且如果你用的谷歌浏览器已经是打开的，就要重新关闭后打开。此链接在出现故障后也许有帮助 http://xieshaohu.wordpress.com/2010/10/11/ubuntu-10-10-marverick-%E4%BD%BF%E7%94%A8gogoc%E6%9B%BF%E4%BB%A3gw6c%E8%BF%9E%E6%8E%A5ipv6/				


## 法二：自建VPS SSR服务器				

## 法三：购买支持IPv6的VPN					

## 法四：Opera浏览器自带VPN		
* 下载安装：https://www.opera.com/zh-cn
* 设置系统区域		
	* Windows直接进入控制面板——区域和语言，将国家或地区设置为：中国台湾（在墙外的都可以）		
* 开启福利功能
	* 同样是进入opera浏览器设置页，点击 **隐私&安全** 把福利功能勾选启用即可
* 开启科学上网
 * 这时在浏览器地址栏前面会出现蓝色的V屁恩的字样，说明V屁恩已经启用，我们可以点击它，查看流量，快速打开和关闭，更改服务器位置等操作。
 * 实测看YouTube速度一般，能看480P或720P，1080P以上还是别抱有太大期望。 

* 关键在于两点：一是更改计算机默认位置到国外，二是更改浏览器默认语言，才会出现标题中的隐藏福利功能：V屁恩启用项。
设置好之后，浏览器的语言改回简体中文不影响。

PS：检测DNS是否被污染：http://www.webdnstools.com/dnstools/dns-lookup				

参考：		
[1] http://blog.51cto.com/happylifeboy/516574			
[2] https://zhuanlan.zhihu.com/p/21434968			
[3] https://www.linuxidc.com/Linux/2013-06/86562.htm			

