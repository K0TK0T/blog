---
title: 在GitHub上使用Hexo搭建个人博客（2021.3，raspberry pi 4b）
tags:
    blog
    github
categories: blog
date: 2021-3-29 18:00:00
top: true
---

### 1、Git，GitHub和Hexo

* **Git**

Git是一个版本控制系统，它安装在你的计算机上，用于管理工程。比如电脑上有一个正在开发的项目，怕它出点什么意外损坏丢失，就可以把它初始化为一个Git仓库，这样Git就可以保存它的历史版本，同时可以在保留主分支的情况下切换到其他分支工作。Git不仅可以用来管理代码，还可以用来管理其他的文件，比如照片office文档等等，和GitHub等托管网站一起使用可以做到跨平台同步和多人协作。

* **GitHub**

Git项目托管平台，支持Git作为唯一的版本库格式进行托管。GitHub中的每一个repository都对应一个Git仓库（也就是初始化过，文件夹下有.git的目录），通过pull、push等操作和主机进行数据交换。

* **Hexo**

静态博客网站生成器，注意是生成器，不是框架，直接把它push到username/username.github.io.git是不会显示网页的。可以把它想象成一个博客后台，写完mrakdown放在/sources/_posts/，想要发布就运行`hexo generate & hexo deploy`。

<!--more-->

* node.js

基于Chrome V8的JavaScript Runtime，Hexo的运行环境，一起安装的npm是一个相当强大的软件包管理器。

* Markdown

一种文本标记语言，可以说在HTML顶层，兼容HTML语法。Mrakdown语法简洁，并且易于阅读和维护，毕竟写博客的时候一大堆HTML标签的排版问题会让人很头疼。Mrakdown最终还是翻译为HTML显示在网站中。

### 2、它们如何协作
简言之就是Git用来管理Hexo项目以及把它生成的静态网页发送到GitHub上，然后由GitHub托管你的博客网站。

GitHub有一个很好用的功能，就是可以用username.github.io作为域名访问username.github.io.git仓库下的网站。最简单的玩法，在你的GitHub账户中建立名字为username.github.io的仓库，push进去index.html，访问username.github.io出现的就是index.html的页面。如果换一个浪漫一点的域名，在网页上画一个爱心，甚至能用来表白 orz。

### 3、安装Hexo，生成博客框架
这一部分[官网文档](https://hexo.io/zh-cn/docs/)有详细说明，不同操作系统可以自己查找。
这里是linux nodejs发行版本网址[nodesourse](https://github.com/nodesource/distributions)。

* 安装node.js

```bash
curl -fsSL https://deb.nodesource.com/setup_15.x | sudo -E bash -
sudo apt-get install -y nodejs
```

* 安装Hexo

```bash
npm install hexo-cli -g
```

* 生成网站框架,在blog/public下

```bash
mkdir ~/blog & cd ~/blog
hexo init
npm install
```

* 设置_config.yml参数，主要是#Site部分。这些会显示在你的博客首页。

```
title: Blabla
subtitle: ''
description: ''
keywords:
author: blabla
language: zh-CN #！
timezone: 'Asia/Shanghai' #！
```

* 本地测试，这时应该显示默认主题landscape和/source/_posts下的hello-world.md。

```bash
hexo generate
hexo server
curl http://localhost:4000  #或者直接浏览器访问
```

### 4、安装Git，设置GitHub，部署静态网页

* 安装Git并设置本地用户名和密码（这和你的GitHub账号无关，但是还是要设置之后才能传输文件到远程库，代表是谁提交的修改）

```bash
sudo apt install git
git config --global user.name "Your Name"
git config --global user.email “email@example.com”
```

* 在GitHub建立远程仓库username.github.io（Your repositories -> new，repository name填username.github.io）
* 与远程仓库建立连接

```bash
ssh-keygen -t rsa
```

将.ssh/id_rsa.pub里的内容粘贴到GitHub的Settings->SSH and GPG keys->new SSH key里保存。

* 设置_config.yml，更改url和deploy部分，使得hexo能部署到你的GitHub页面。

```
url: https://github.username.io

deploy:
	type: git
	repo: https://github.com/username/username.github.io
	branch: main
```

* 安装部署工具，部署网页，这一步完成博客就算建好了，可以通过域名访问。

```bash
npm install hexo-deployer-git --save
hexo generate
hexo deploy
```

* 官方文档中还给出了使用Travis CI部署的方式，大概是每次你将主分支提交修改的时候都会向travis也发送一份，travis在远程服务器完成你指定的一系列操作后再将形成好的静态网页发送到你的gh-pages分支下，将你的仓库设置为gh-pages分支就可以实现每次push之后部署，不过官方给的文档里就有很多错误比如master分支早就改为main了，从头到尾都没看到gh-pages等等，有兴趣的话可以自己研究试试。一方面travis登录要梯子，国内操作不方便，另一方面半懂不懂的做完以后可能会出现更大的问题，我就干脆不管，直接手动部署算了。

### 5、安装主题，撰写博客

这一部分就比较轻松，Hexo的主题[在这](https://hexo.io/themes/)，大部分的主题在他们的代码仓库里找就能找到，方法就是把域名（username.github.io）里的username放到github.com/username里直接访问就好，基本上都有安装说明。大致步骤`git clone xxx.git ~/blog/themes/xxx`，`npm install`，再在_config.yml设置主题`theme: xxx`。

写博客和前面说的一样，写好markdown放在blog/source/_post下，或者运行`hexo new "new-file-name"`也行（想要删除帖子直接把md文件删除就好），全部整理好之后`hexo generate & hexo deploy`，过半分钟再去看就更新了。

### 6、常用命令合集
整理了一些写博客时常用的命令。

* Hexo初始化

```bash
hexo init [dir]
npm install
```

* 安装主题

```bash
git clone "xxx.git" ~/blog/xxx
npm install
```

* 部署网站

```bash
hexo generate
#hexo server
hexo deploy
```

* 管理Git仓库

```bash
git init
git status
git add .
git commit -m ""
git remote add origin "xxx.git"
git pull
git push
```

