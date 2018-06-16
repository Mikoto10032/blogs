---
date: 2018-06-14
title: "GitHub IO配合HuGo搭建个人静态博客"
tags:
    - 博客
    - 建站
    - Github
categories:
    - 程序员那些事
comment: true
---

# 准备工作
* 必须创建一个仓库，名称为**username.github.io**，创建过程参考[该博客](https://keysaim.github.io/post/blog/2017-08-15-how-to-setup-your-github-io-blog/)
* 创建一个仓库用来存放博客,名称随意，作者这里就命名为**blogs**
* 创建一个仓库用来存放博客的评论（如果想要添加评论功能），作者这里就命名为**BlogsComments**		

# 开始搭建	    	
## 安装Hugo	

### Windows用户	
如果你安装了**Chocolatey**，那么你就可以执行如下命令来一键安装：`choco install hugo -confirm`		

否则，就要手动安装：			
* 安装[Go](https://golang.org/doc/install?download=go1.10.3.windows-amd64.msi)
* 创建相应文件夹			
	* 创建 D:\Hugo 文件夹
	* 创建 D:\Hugo\bin 文件夹
	* 创建 D:\Hugo\Sites 文件夹
*  下载安装Hugo	
	* 下载Windows版本最新的[Release](https://github.com/gohugoio/hugo/releases)	
	* 将文件解压到 D:\Hugo\bin\	
	* 将exe可执行文件重命名为**hugo.exe**	
	* 将hugo.exe的全路径添加至你的系统环境变量，确认你能在cmd窗口下执行`hugo help`命令
* 至此，Hugo安装完毕

### MAC用户	
Hugo安装十分简单，在MAC的终端执行命令：
`brew install hugo`
## 测试Hugo	
* cmd下依次执行如下命令		
	* `cd C:\Hugo\Sites`
	* `hugo new site example.com`
* 现在生成了C:\Hugo\Sites\example.com的目录
* 可以本地查看静态网页

## 用Hugo建站		
### 初始化博客站			
`hugo new site blogs`		
### git init	
* `cd blogs`
* `git init`

### 指定github源		
* `git remote add origin git@github.com:Mikoto10032/blogs.git`

## 添加主题 	

		git submodule add -b master https://github.com/xianmin/hugo-theme-jane.git themes/jane
		cp -r themes/jane/exampleSite/content ./			
		cp themes/jane/exampleSite/config.toml ./
## 本地测试	
`hugo server`		
打开浏览器，访问[http://localhost:1313](http://localhost:1313)		
## 修改默认配置（config.toml）		
### 修改baseurl		
baseURL是你博客最终部署的网站的url，基于github.io的话就应该是这样的[https://Mikoto10032.github.io/](https://Mikoto10032.github.io/)
### 启用gitment评论			
* 申请[OAuth application](https://github.com/settings/applications/new)		
	* Application name填写应用名称，随意
	* Homepage URL，主页地址，不太重要，建议填写博客地址
	* Application description，随意
	* **Authorization callback URL**，务必填写[https://Mikoto10032.github.io/](https://Mikoto10032.github.io/),即是你的github.io的地址
	* 在[https://github.com/settings/developers](https://github.com/settings/developers)可以查看你的授权账号和授权密码
* 配置params.gitment		
 
		[params.gitment]          # Gitment is a comment system based on GitHub issues. see https://github.com/imsun/gitment
    	owner = "Mikoto10032"              # Your GitHub ID，例如Mikoto10032
    	repo = "BlogsComments"               # The repo to store comments
    	clientId = "xxxx"           # Your client ID
    	clientSecret = "xxxx"       # Your client secret
* 修改博文显示数量	

		paginate = 15               # 首页每页显示的文章数
		archive-paginate = 50       # 归档、标签、分类每页显示的文章数目
* 修改语言		
修改成中文：	
	
		defaultContentLanguage = "zh-cn"
		[Languages.zh-cn]
  		languageCode = "zh-cn"

## 编辑博客		
默认情况下，Jane主题将博文放在content/post/下面，你需要在这下面编辑你的博文。Hugo是支持分目录的，这点非常好		
博客的头部可以这样子写：

		---
		date: 2018-03-22
		title: "如何在github.io搭建Hugo博客"
		tags:
		- 教程
		- github
		categories:
		- github
		comment: true
		---
编辑完成后可以git提交：

	git add xxxx
	git commit -m "YOUR COMMIT MESSAGE"
	git push origin master
## 部署博客站
### 添加github.io
当前工作目录是Sites\blogs		

	git submodule add -b master git@github.com:keysaim/keysaim.github.io.git public
这里将其作为submodule添加进来，且放到public目录下面，public目录是Hugo生成静态文件的地方，这样的话咱们就可以把生成出来的静态文件直接上传到你的<username>.github.io的repo里面了
### 生成静态博客站
`hugo`
直接运行hugo命令，就会在public目录下生成静态博客站。
### 提交

	cd public
	git add .
	git commit -m "YOUR COMMIT MESSAGE"
	git push origin master
### 查看你的github.io博客站
正常情况下，过一会你就可以看到你基于Hugo的github.io博客站了，作者的是[https://mikoto10032.github.io](https://mikoto10032.github.io)

## 日常操作流程	

	日常操作流程：
	cd blogs
	content下写好文章
	hugo
	git add .
	git commit
	git push origin master
	cd public
	git add .
	git commit
	git push origin master
至此，恭喜你已经完成了你的Hugo博客站了。