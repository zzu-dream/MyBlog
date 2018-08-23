---
title:  git 如何删除缓存的远程分支列表.md
tags:  [git删除缓存远程分支]
categories:  [git]
date:  2018-06-11 16:17:22
---

[常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)

## 列出远程分支

使用git 部署代码，<pre> git branch -a </pre> 里面列出的很多远程的分支，其实都是已经被删除了的。

## 删除缓存的远程分支列表
用此命令：
``` git
git remote prune origin
or
git fetch -p   
```
即可解决

## 列出提交个数
```
git rev-list --count HEAD
```