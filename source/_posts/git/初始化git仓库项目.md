---
title:  初始化git仓库项目.md
tags:  [git仓库]
categories:  [git]
date:  2018-06-11 16:17:22
---

[常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
# Command line instructions 命令行指令


## Git global setup

```
git config --global user.name "xxx"
git config --global user.email "xxx@email.com"
```
## Create a new repository

```
git clone git@git.jd.com:xxx/yyy.git
cd JDViewKitDoc
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

## Existing folder

```
cd existing_folder
git init
git remote add origin git@git.jd.com:xxx/yyy.git
git add .
git commit -m "Initial commit"
git push -u origin master
```
## Existing Git repository

```
cd existing_repo
git remote add origin git@git.jd.com:xxx/yyy.git
git push -u origin --all
git push -u origin --tags
```

## 问题解决方案

### fatal: refusing to merge unrelated histories 解决方案

#### 解决方案

可以使用 rebase 的方式来进行合并。

```
git pull --rebase origin master

```

```
cd
mkdir rebaseTmp
cd rebaseTmp
echo "hello a line" > tmp.txt
git init
git add .
git commit -m "Local first commit"
git remote add origin  https://github.com/HustLion/java_console_log4j.git
git pull --rebase origin master

git push -u origin master
```
