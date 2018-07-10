---
date: 2018-06-29
title: "VPS基于LAMP搭建Aria2+AriaNg+Nextcloud"
tags:
    - 建站
    - VPS
    - Aria2
    - NextCloud
    - LAMP
categories:
    - 程序员那些事
comment: true
---

# 一、安装Aria2	

## 1.下载安装aria2
ubuntu系统：		

	apt-get update
	apt-get install aria2	
centos：	

    yum install epel-release
    yum install aria2

## 2.aira2配置			
* **先创建目录和文件**

```    
mkdir /aria2
cd /aria2
vi aria2.conf
```

* **编辑aria2.conf**	

```	
#允许rpc
enable-rpc=true
#允许所有来源, web界面跨域权限需要
rpc-allow-origin-all=true
#允许非外部访问
rpc-listen-all=true
#RPC端口, 仅当默认端口被占用时修改
#rpc-listen-port=6800
 
#用户名
rpc-user=susu
#密码
rpc-passwd=138vps

#RPC密钥
#rpc-secret=138vps
###速度相关 
#最大同时下载数(任务数), 路由建议值: 3
max-concurrent-downloads=5
#断点续传
continue=true
#同服务器连接数
max-connection-per-server=5
#最小文件分片大小, 下载线程数上限取决于能分出多少片, 对于小文件重要
min-split-size=20M
#单文件最大线程数, 路由建议值: 5
split=10
#下载速度限制 0 不限制
max-overall-download-limit=0
#单文件速度限制
max-download-limit=0
#上传速度限制
max-overall-upload-limit=0
#单文件速度限制
max-upload-limit=0
#断开速度过慢的连接
#lowest-speed-limit=0
#验证用，需要1.16.1之后的release版本
#referer=*
 
###进度保存相关 
input-file=/root/aria2.session
save-session=/root/aria2.session
#定时保存会话，需要1.16.1之后的release版
#save-session-interval=60
 
###磁盘相关 
#文件保存路径, 默认为当前启动位置
dir=/var/www/html/
#文件缓存, 使用内置的文件缓存, 如果你不相信Linux内核文件缓存和磁盘内置缓存时使用, 需要1.16及以上版本
#disk-cache=0
#另一种Linux文件缓存方式, 使用前确保您使用的内核支持此选项, 需要1.15及以上版本
#enable-mmap=true
#文件预分配, 能有效降低文件碎片, 提高磁盘性能. 缺点是预分配时间较长
#所需时间 none < falloc ? trunc << prealloc, falloc和trunc需要文件系统和内核支持
file-allocation=prealloc
 
###BT相关 
#启用本地节点查找
bt-enable-lpd=true
#添加额外的tracker
#bt-tracker=<URI>,…
#单种子最大连接数
#bt-max-peers=55
#强制加密, 防迅雷必备
#bt-require-crypto=true
#当下载的文件是一个种子(以.torrent结尾)时, 自动下载BT
follow-torrent=true
#BT监听端口, 当端口屏蔽时使用
#listen-port=6881-6999
#aria2亦可以用于PT下载, 下载的关键在于伪装
#不确定是否需要，为保险起见，need more test
enable-dht=false
bt-enable-lpd=false
enable-peer-exchange=false
#修改特征
user-agent=uTorrent/2210(25130)
peer-id-prefix=-UT2210-
#修改做种设置, 允许做种
seed-ratio=0
#保存会话
force-save=true
bt-hash-check-seed=true
bt-seed-unverified=true
bt-save-metadata=true
#定时保存会话，需要1.16.1之后的某个release版本
#save-session-interval=60
```    	
* **启动aria2**		

```
aria2c --conf-path=/aria2/aria2.conf -D
aria2c --enable-rpc --rpc-listen-all=true --rpc-allow-origin-all -c -D
```
* PS：貌似重新启动后要重新启动aria2？

# 二、安装AriaNg管理面板			

*PS:如果想在服务器上安装管理面板，那么就安装Apache，否则直接下载[AriaNg项目](https://github.com/mayswind/AriaNg/releases/download/0.4.0/aria-ng-0.4.0.zip)到本地访问即可，配置信息看下面*

## 1.Apache安装			

ubuntu系统：

    apt-get -y install apache2

centos：	

    yum  -y  install  httpd
    chkconfig --levels 235 httpd on
    service httpd start
    
## 2.安装下载AriaNg	
* 输入命令：

```
wget http://dl.138vps.com/linux/ariang.tar.gz
```

* 解压	：

```
tar zxvf ariang.tar.gz		
```

* 移动到Apache网站目录：

```    
cp -r ./ariang /var/www/html	
```
* 修改权限：

```
chmod 755 /var/www/html/ariang	
```

* 访问：

```
http://IP地址/ariang			
```
* 配置：
AriaNg设置->RPC设置（填写ip，如果有rpc-secret就填写）

# 三、安装NextCloud	

##	1.手动安装(还是手动安装好)		

### （1）LAMP安装			
	
一键LAMP安装：`apt-get install apache2 php7.0 mysql-server`	
再安装一些也许需要的PHP模块：	

```
apt-get install apache2 libapache2-mod-php7.0 php7.0-gd php7.0-mysql 
php7.0-curl php7.0-intl php7.0-mcrypt php-imagick php7.0-zip php7.0-xml php7.0-mbstring
```

###	（2）配置数据库		

```
#登录mysql
mysql -u root -p                 

#创建名为nextcloud的数据库
mysql> CREATE DATABASE nextcloud;
Query OK, 1 row affected (0.01 sec)

#切换数据库
mysql> USE nextcloud
Database changed

#创建名为nextcloud的用户，密码为password，并赋予相关权限
mysql> GRANT All  ON nextcloud.* TO nextcloud@localhost IDENTIFIED BY 'password'; 
Query OK, 0 rows affected, 1 warning (0.00 sec)

#登出mysql
mysql> exit
Bye
```

### （3）Nextcloud安装		
* 下载安装包		

```
wget https://download.nextcloud.com/server/releases/nextcloud-13.0.4.zip
```
* 解压	

```
unzip nextcloud-13.0.4.zip
```
* 移动到Apache网站目录

```
cp -r nextcloud /var/www/html
```
* 访问 `ip/nextcloud`	

* 填写信息即可		

### 常见问题		
* 内部服务器错误			

原因：nextcloud权限设置问题
解决：设置nextcloud的拥有者和权限			
```
chown www-data /var/www/html/nextcloud
chmod 775 /var/www/html/nextcloud
```
* 无法创建或写入数据目录 xxx		

原因：也是权限问题
```
chown www-data /mydownload
chmod 775 /mydownload
```

```
chmod 770 /var/www/html/nextcloud -Rf & chown www-data /var/www/html/nextcloud -Rf
```
* 刷新网页后，提示有模块未安装	

```
apt-get install php7.0-zip php7.0-dom php7.0-xml php7.0-gd php7.0-curl php7.0-mysql
service apache2 restart
```
*PS：
（1）主要是两个地方：数据目录和数据库配置。数据目录要填写绝对目录，最后不带“/”，而且要保证这个目录至少拥有750权限、用户名和组为www-data。数据库这要填写之前使用phpMyAdmin所设置的用户名和数据库。
（2）如果提示数据库访问错误，可以试试换成root用户（虽然这样做不安全）*

## 2.Snap安装（貌似snap安装了nextcloud后apache就不起效了？？？） 	

* snap是什么？

```    
#查看snap版本信息
snap --version
#找出所有snap应用
snap find
#安装应用
snap install 包名
#重启应用
snap restart 应用名
#升级应用
snap refresh 应用名
#查看安装的应用
snap list
#卸载应用
snap remove 应用名	
```
* 安装	

```  
#更新系统
apt-get update -y
#安装NextCloud
snap install nextcloud		
```
* http://your_ip 进入登录页面		


* **将aria2的下载目录改成snap的数据目录后nextcloud就可以查看aria2下载的文件了**	
目录是：`/var/snap/nextcloud/common/nextcloud/data`		

PS：[aria2实现下载上传到GoogleDrive](https://mikoto10032.github.io/post/%E7%A8%8B%E5%BA%8F%E5%91%98%E9%82%A3%E4%BA%9B%E4%BA%8B/aria2%E7%A6%BB%E7%BA%BF%E4%B8%8B%E8%BD%BD%E5%B9%B6%E4%B8%8A%E4%BC%A0%E5%88%B0gooledrive/)			

参考：			
[1] [https://www.orgleaf.com/2203.html](https://www.orgleaf.com/2203.html)				
[2] [https://www.orgleaf.com/2224.html](https://www.orgleaf.com/2224.html)			
[3] [https://wzfou.com/nextcloud-aria2/](https://wzfou.com/nextcloud-aria2/)