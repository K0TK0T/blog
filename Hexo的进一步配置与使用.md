---
title: Hexo的进一步配置与使用
date: 2021-04-01 15:12:53
tags:
- hexo
- blog
- NexT
categories:
- blog
---

### 1、安装[NexT](https://github.com/theme-next/hexo-theme-next)主题与个人信息配置

* 安装

```bash
cd blog
git clone https://github.com/theme-next/hexo-theme-next themes/next
vim _config.yml
:%s/landscape/next
```

* 个人信息配置（其他的个人信息在项目根目录的_config.yml下）

```bash
vim themes/next/_config.yml
```

1. favicon（也就是显示在你的浏览器标签页左边的小图标）

```
favicon:
  small: /images/favicon-16x16-next.png
  medium: /images/favicon-32x32-next.png
  apple_touch_icon: /images/apple-touch-icon-next.png
  safari_pinned_tab: /images/logo.svg
  #android_manifest: /images/manifest.json
  #ms_browserconfig: /images/browserconfig.xml
```

2. scheme（next的主题样式，注意第三个Pisces可能部署不了，尽量不要选，前两个主题不是平铺，一言难尽...）

```
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini
```

4. avatar（侧边栏头像）

```
avatar:
  # Replace the default image and set the url here.
  url: #/images/avatar.gif
  # If true, the avatar will be dispalyed in circle.
  rounded: false
  # If true, the avatar will be rotated with the cursor.
  rotated: false
```

5. social（社交链接，比如说github、csdn、简书、qq等等，后面的图标可以在[这里](https://fontawesome.com/icons)找，改||后的内容就好）

```
social:
  #GitHub: https://github.com/yourname || fab fa-github
  #E-Mail: mailto:yourname@gmail.com || fa fa-envelope
  #Weibo: https://weibo.com/yourname || fab fa-weibo
  #Google: https://plus.google.com/yourname || fab fa-google
  #Twitter: https://twitter.com/yourname || fab fa-twitter
  #FB Page: https://www.facebook.com/yourname || fab fa-facebook
  #StackOverflow: https://stackoverflow.com/yourname || fab fa-stack-overflow
  #YouTube: https://youtube.com/yourname || fab fa-youtube
  #Instagram: https://instagram.com/yourname || fab fa-instagram
  #Skype: skype:yourname?call|chat || fab fa-skype
  CSDN: https://www.csdn.net/yourname || fab fa-cuttlefish
```

6. footer（尾注，显示你的版权信息等等，把powered设置为false可以不显示Powered by Hexo & NexT，也可以定制下面那个心型小图标）

```
footer:
  # Specify the date when the site was setup. If not defined, current year will be used.
  #since: 2015
  # Icon between year and copyright info.
  icon:
    # Icon name in Font Awesome. See: https://fontawesome.com/icons
    name: fa fa-heart
    # If you want to animate the icon, set it to true.
    animated: false
    # Change the color of icon, using Hex Code.
    color: "#ff0000"
  # If not defined, `author` from Hexo `_config.yml` will be used.
  copyright:
  # Powered by Hexo & NexT
  powered: true
```



### 2、添加标签和分类等侧边栏

* 修改themes/next/_config.yml，把需要的项目前面的注释取消，图标不满意依然可以在[这里](https://fontawesome.com/icons)找。

```
menu:
  home: / || fa fa-home
  #about: /about/ || fa fa-user
  #tags: /tags/ || fa fa-tags
  #categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-gamepad
  #schedule: /schedule/ || fa fa-calendar
  #sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```

* 创建对应的文件夹和index.md，比如about，运行下面的命令可以自动创建这些。

```bash
hexo new page about
```

* 特殊的tags和categories只要在front-matter部分加上这一行就会自动生成，不需要多加什么。

```
type: tags
# type: categories
```



### 3、通过Leancloud给博客添加浏览量统计功能和评论功能

在[leancloud](https://www.leancloud.cn/)建立两个应用，分别命名为counter和quote，前者是浏览量统计，后者是评论。在两个应用的setting->app keys可以找到它们的AppID和AppKey。

* leancloud浏览量统计

```
leancloud_visitors:
  enable: false
  app_id: # <your app id>
  app_key: # <your app key>
  # Required for apps from CN region
  server_url: # <your server url>
  # Dependencies: https://github.com/theme-next/hexo-leancloud-counter-security
  # If you don't care about security in leancloud counter and just want to use it directly
  # (without hexo-leancloud-counter-security plugin), set `security` to `false`.
  security: true
```

1. 将enable设置为true
2. 将counter应用的appid和appkey填进去
3. 解决依赖插件，`npm install hexo-leancloud-counter-security --save `
4. 将security设置为false



* Valine评论功能

```
# Valine
# For more information: https://valine.js.org, https://github.com/xCss/Valine
valine:
  enable: false
  appid: # Your leancloud application appid
  appkey: # Your leancloud application appkey
  notify: false # Mail notifier
  verify: false # Verification code
  placeholder: Just go go # Comment box placeholder
  avatar: mm # Gravatar style
  guest_info: nick,mail,link # Custom comment header
  pageSize: 10 # Pagination size
  language: # Language, available values: en, zh-cn
  visitor: false # Article reading statistic
  comment_count: true # If false, comment count will only be displayed in post page, not in home page
  recordIP: false # Whether to record the commenter IP
  serverURLs: # When the custom domain name is enabled, fill it in here (it will be detected automatically by default, no need to fill in)
  #post_meta_order: 0
```

1. 将enable设置为true
2. 将应用quote的appid和appkey填进去
3. 下面看着设置，一般要把language设置为zh-cn



### 4、添加置顶功能

```bash
npm remove hexo-generator-index
npm install hexo-generator-index-pin-top --save

# 如果想给置顶贴加一个置顶标志
vim /blog/themes/next/layout/_macro/post.swig
```

在`<div class="post-meta">`标签内添加下面的内容

```
{% if post.top %}
    <i class="fa fa-thumb-tack"></i>
    <font color=green>置顶</font>
    <span class="post-meta-divider">|</span>
{% endif %}
```

使用置顶功能的方法是在文章的front-matter部分加上

```
top: true
# 或者数字，数字越大，优先级越高
top: 5
```



### 6、添加站内搜索

```bash
npm install hexo-generator-searchdb
vim /themes/next/_config.yml
```

把local_search的enable选项设置为true



### 7、其他小技巧

1. themes/next/_config.yml的motion标签设置为false可以禁用动画效果，节省加载时间。

2. themes/next/_config.yml的font标签可以设置博客各部分的字体。

