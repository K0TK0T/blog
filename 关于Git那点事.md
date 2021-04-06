---
title: 关于Git那点事
date: 2021-04-03 12:59:02
tags:
- git
categories:
- git
---

### 1、初始化Git仓库

```bash
cd gitrepo
git init
git add .  # 本地添加修改
git status
# 设置本地用户名和邮箱
git config --global user.name "name"
git config --global user.email "eamil-address"
git commit -m "first commit"  # 本地提交修改
git branch -M main  # 给分支改名为main
```

### 2、链接到远程库

```bash
ssh-keygen -t rsa  # 生成ssh公钥和私钥，将公钥存放到github公钥中
git remote add origin <url>  # 添加远程仓库
git push -u origin main  # 推送分支
```

### 3、分支操作

```bash
git branch  # 查看本地分支
git branch -a  # 查看本地和远程的所有分支

git branch [branch_name]  # 新建分支
git branch -m [branch_name]  # 移动/重命名分支（-M强制移动，即使没有完全合并）
git branch -d [branch_name]  # 删除分支（-M强制删除，即使没有完全合并）

git checkout [branch_name]  # 切换分支（-b同时创建分支）
git diff [branch_name]  # 比较分支
git merge [branch_name]  # 合并分支
git push -u origin [branch_name]  # 提交分支，再次提交就不需要后面的参数了，-u就是--set-upstream，设置提交流
```

### 4、解决远程冲突

```bash
git fetch origin [branch_name]:[dev]  # 将远程分支拉到本地的另一条分支上
git diff [dev]  # 比对本地和远程分支
git merge [dev]  # 合并分支
git push  # 重新提交
git branch -d [dev]  # 删除远程分支
```

