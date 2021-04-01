---
title: 在Ubuntu上安装Typora（2021.3，Ubuntu 16.04）
tags:
- ubuntu
- typora
categories:
- ubuntu
date: 2021-3-31 18:00:00
---

### 1、通过官方给的软件源安装

```bash
# 将typora仓库的key添加到你的apt-key中
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -
# 在你的软件源里添加typora仓库
sudo add-apt-repository 'deb https://typora.io/linux ./'
# 更新软件源列表，安装typora
sudo apt-get update
sudo apt-get install typora
```

大多数人都会卡在这里，因为https://typora.io 这个服务器在国外，除非有映射到socks5协议，命令行工具可以使用的代理才能下载下来这个软件包。相关配置很麻烦，而且不适合在博客里写，所以有兴趣可以想办法百度或者Google。如果你已经跟着官网运行了上面的命令行不知道怎么办了的话，可以通过下面的操作解决一些问题：

* 清除安装不完全的Typora包

```bash
# 如果正在下载中，可以通过Ctrl+C强制退出
sudo apt autoclean
```

* 删除Typora的仓库，以免以后软件源更新的时候出问题

```bash
# 是不是很熟，更换国内源的时候也是在这里，当然Ubuntu有更简便的方式
sudo vim etc/apt/sources.list
# 删除最下面几行有typora的链接
sudo apt update
```

<!--more-->

### 2、通过官方提供的tar ball手动安装

这个稍微能下动一点，缺点是需要手动配置的地方多，比较麻烦。

```bash
# 下载typora的tar ball，当然也可以直接在官网点download binary file下载
wget https://typora.io/linux/Typora-linux-x64.tar.gz
# 将里面的内容解压到/usr/local下，也就是Ubuntu默认的用户软件目录
sudo tar -zxvf Typora-linux-x64.tar.gz -C /usr/local/
# 在/usr/local/bin中创建typora的软链接，以便可以在命令行中调用
sudo ln -s /usr/local/Typora-linux-x64/Typora /usr/local/bin/typora
# 创建typora的desktop文件，这样就可以在图形界面调用，毕竟给的安装包里没有
sudo touch /usr/share/applications/Typora.desktop
```

这里是一个Typora.desktop样例：[转自CSDN](https://blog.csdn.net/qq_41477556/article/details/113689208)

```
Desktop Entry]
Encoding=UTF-8
Name=Typora
Exec=/usr/local/Typora-linux-x64/Typora
Icon=//usr/local/Typora-linux-x64/resources/app/asserts/icon/icon_256x256@2x.png
Categories=Application;Development
Type=Application
#Terminal=1
```



### 3、通过deb包安装

当然这个是最简便也最省事的，记得第一个方法吗，它其实就是抓取仓库里的deb包到你的电脑上安装，这个url是https://typora.io/linux/linux/typora_0.9.98_amd64.deb （0.9.98版本，这个链接在通过官方给的软件源安装的过程可以看到），可见Typora的安装其实给你绕了一个大圈。总之我想尽办法把它下载下来了，用dpkg安装就好。

```bash
dpkg -i typora_0.9.98_amd64.deb
```

[网盘链接](https://pan.baidu.com/s/1gKWB7STFwdW6bNOhpcmm1g)：提取码`jw10`