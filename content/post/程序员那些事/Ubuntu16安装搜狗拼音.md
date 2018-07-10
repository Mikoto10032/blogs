---
date: 2018-07-10
title: "Ubuntu16安装搜狗拼音"
tags:
    - 环境配置
    - Linux
categories:
    - 程序员那些事
comment: true
---
# 前情提要			
在安装之前，我们要先了解一个事实，那就是linux下安装软件和Windows是非常不同的，并不是简单地双击安装包就可以安装了。linux很多软件都有自己的一个依赖源，如果不先安装好这些依赖源，你是无法成功安装软件的。那么搜狗输入法就需要依赖fcitx这个框架。

【fcitx是 (Free Chinese Input Toy for X) 的英文缩写，中文名为小企鹅输入法，是一个以 GPL 方式发布的输入法框架， 编写它的目是为桌面环境提供一个灵活的输入方案，彻底解决在GNU/Linux下没有一个好的中文输入法的问题。】		

# 一、一般安装方式			

1. Ctrl+Alt+T，打开终端Terminal；

2. 先添加以下源，在终端输入命令：sudo add-apt-repository ppa:fcitx-team/nightly

3. 更新一下系统给，继续输入命令：sudo apt-get update

4. 安装fcitx，输入命令：sudo apt-get install fcitx

5. 安装fcitx的配置工具，输入命令：sudo apt-get install fcitx-config-gtk

6. 安装fcitx的table-all软件包，输入命令：sudo apt-get install fcitx-table-all，遇到”希望继续执行吗“选择Y

7. 安装im-switch切换工具，输入命令：sudo apt-get install im-switch，遇到”希望继续执行吗“选择Y

8. 安装完成了，然后点击桌面左上角在计算机中搜索fcitx，如果能找到说明安装成功了

9. 安装搜狗输入法：假设你的安装包放在Downloads文件夹下，那么在终端输入命令：
(0)`wget http://cdn2.ime.sogou.com/dl/index/1524572264/sogoupinyin_2.2.0.0108_amd64.deb?st=2HtnuwOvQDfamw_7BmjGXA&e=1530674626&fn=sogoupinyin_2.2.0.0108_amd64.deb`
(1)ls
(2)cd Downloads/
(3)ls  (这个时候就会列出你的Downloads文件夹下都有哪些安装包)

(4)sudo dpkg -i sogoupinyin_XXXX.deb			

# 二、fcitx依赖			
`sudo apt-get install -f`		
`reboot`

# 三、配置搜狗拼音		

1. 首先打开右上角系统设置，选择第一行的最后一个选项”Text Entry“；

2. 点击左下角的+号，在打开的窗口中找到搜狗输入法Sogou pinyin点击Add添加进去			
![](https://img-blog.csdn.net/20170508152859857?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd29haW5pc2hpZnU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)			
3. 这时就可以看到列表中有搜狗输入法了。这个时候再打开fcitx的配置窗口，点击左下角的+号再列表中选择搜狗输入法添加进来：
![](https://img-blog.csdn.net/20170508153116121?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd29haW5pc2hpZnU=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
PS：去掉 only show current language 的√查看sougoupinyin			
4. 添加成功了，把搜狗输入法移动到第一的位置。看看你的桌面右上角输入法那个地方，是不是出现搜狗输入法了！

