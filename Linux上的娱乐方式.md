---
title: Linux上的娱乐方式（2021.3，Ubuntu Mate 20.04）
date: 2021-04-08 14:18:46
tags:
- linux
- game
categories:
- game
---

>*很多人认为Linux是很无趣的，只能用于研究和工作的开发用系统。如果这句话放在四年前确实是，因为当时大多数软件对Linux的支持都处于一个起步阶段，稳定性差，原生支持少，想在Linux上玩游戏和处理日常事务很困难。不过经过了几年的发展，渐渐形成了体系，比如国内的百度网盘、WPS、QQ音乐、网易云音乐在LInux平台上线，Steam上steamox+linux的游戏增加，RetroPie的出现，Flathub的大幅度完善等等。Linux早就不是当年配置软件源就要敲半天的蹩脚系统，非常容易配置和使用。*



## 游戏篇

### Steam

别说，Steam上面还有挺多好游戏的，简单举几个例子：弹丸论破1+2、星露谷物语、泰拉瑞亚、饥荒、命运石之门、寒蝉鸣泣之时、去月球、Undertale、空洞骑士、古墓丽影、蔚蓝、死亡细胞、武士刀零、杀戮尖塔。具体的可以在商店->浏览->SteamOS+Linux分类下浏览，当然如果电脑配置并不高，最好还是玩文字类游戏，动作类会很卡。

[![cYSuO1.png](https://z3.ax1x.com/2021/04/08/cYSuO1.png)](https://imgtu.com/i/cYSuO1)

Steam在不同系统上安装总会多多少少出点问题，最常见的是缺少32位库，去百度上搜一下就有解决办法，新内核会自动弹窗提示安装。



### Flathub

flatpak是LInux上的软件包管理器，flathub是它最大的软件库，类似apt和apt库之间的关系吧，不过Flathub提供了可视化的网页检索平台，会比apt在安装应用程序上更有优势。Flathub上有一些Linux原生游戏，比如SuperTuxKart（很不错的赛车游戏）、洞窟物语NX（2D探险，Win、Mac、PSP、3DS和NS都有移植，3DS是3D版本）、Teeworlds（疯狂小人乱斗玩过吧，差不多）等等。除了游戏之外Flathub上还提供一些编译好的模拟器，比如PPSSPP（PSP）、Citra（3DS）和DeSmuME（NDS）。

[![cYkwvD.png](https://z3.ax1x.com/2021/04/08/cYkwvD.png)](https://imgtu.com/i/cYkwvD)



### RetroArch/RetroPie

这个是我在研究树莓派和PSV的时候接触到的，这个RetroArch就是常说的全能模拟器，复古游戏从世嘉到索尼到任天堂几乎无所不能，平台支持广到无法想象，而RetroPie就是使用RetroArch作为一部分开发的复古游戏操作系统，同样支持大多数的游戏平台，具体可以在[这里](https://retropie.org.uk/docs/3do/)查看。RetroPie可以作为应用程序安装。

我个人对GBA、GBC和NDS上的游戏很感兴趣，所以模拟器这部分是我在Linux上的游戏主力了。像火焰纹章、428、塞尔达、符文公房等游戏单里的游戏基本上都是在RetroPie上玩的，要问为什么有实机还要用模拟器，我只能说是掌机画面太小，摇杆按键容易坏，而且要充电不方便吧。

* [RetroArch](https://www.retroarch.com/?page=platforms)

[![cY17Xn.png](https://z3.ax1x.com/2021/04/08/cY17Xn.png)](https://imgtu.com/i/cY17Xn)

是不推荐用这种方法模拟的，因为Linux的RetroArch对中文的支持不好，非常不稳定，配置繁琐，模拟还容易出问题。当初我尝试的时候出现了这些问题：设置中文以后标题和提示乱码，Citra2018模拟时之笛无法设置用户名，mgba模拟缩小帽存档界面不停闪。再加上每一个核心都是有区别的，但是没有区别设置，导致游戏体验特别不好，就直接卸掉了。

* [RetroPie](https://retropie.org.uk/)

[![cYKeUg.png](https://z3.ax1x.com/2021/04/08/cYKeUg.png)](https://imgtu.com/i/cYKeUg)

它有两种安装方式，一种是作为操作系统安装，另一种是作为应用程序安装。

作为操作系统只适用于树莓派，下载镜像烧录在TF卡上，插上去之后就完成了一个简易游戏机。这个方法并不好，因为没有图形界面用于拷贝游戏和管理存档，需要独占一张TF卡，并且需要单独配备外设（屏幕、键盘、鼠标、手柄）。由于国内网络问题，想在RetroPie上安装桌面和添加库挺麻烦，尤其配置网络的时候如果不安装虚拟终端真的会把人看晕的。

作为应用程序安装，文档基本都在[这里](https://retropie.org.uk/download/)，注意只支持Debian系。说一下遇到的坑：1、安装过程要clone国外的git仓库，可能需要外网。2、x86有一两个包实在抓不到，是N64的模拟器，不会影响使用，实在想用就把参数去掉手动clone下来放到`RetroPie-Setup/tmp`对应的位置重新安装（比如lr-desmume-2015）。3、raspi安装比较麻烦，安装失败后需要查看错误日志使用aptitude手动降级一些软件包。

[![cYgDyR.png](https://z3.ax1x.com/2021/04/08/cYgDyR.png)](https://imgtu.com/i/cYgDyR)



### 其他

#### [Citra](https://flathub.org/apps/details/org.citra_emu.citra)

RetroPie可以解决GBA、GBC、Wii、NDS、PSP等等的模拟需求，但是暂时不支持3DS的模拟。Citra可以直接在Flathub上找到编译版本安装，个人认为体验不错。3DS上的经典游戏还是挺多的，像塞尔达三作、重装机兵4、火焰纹章三作等等。

[![cYR2xH.png](https://z3.ax1x.com/2021/04/08/cYR2xH.png)](https://imgtu.com/i/cYR2xH)

#### [ONScripter-jh](https://www.linuxgame.cn/onscripter-jh-ons%E6%A8%A1%E6%8B%9F%E5%99%A8)

ONS文字游戏引擎实现，jh支持了GBK字符。列举一些游戏，比如秋之回忆系列、Key社系列（CLANNAD，Rewirte，LB）、型月系列（FSN，月姬，歌月十夜，魔法使之夜）、AKB系列（车轮之国、G弦）、寒蝉鸣泣之时、海猫鸣泣之时。原作者的发布页面被其本人删掉了，只能在网上找其他方法下载（比如小标题上这个链接）。

[![cYIS8f.png](https://z3.ax1x.com/2021/04/08/cYIS8f.png)](https://imgtu.com/i/cYIS8f)