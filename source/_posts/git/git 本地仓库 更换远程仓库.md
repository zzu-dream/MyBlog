---
title: git 本地仓库 更换远程仓库
tags:  [更换远程仓库]
categories:  [git]
date:  2018-06-11 16:17:22
---

[常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)


## git修改远程仓库地址的三种方法

### 直接命令修改

``` 
git remote set-url origin [url]
```

### 命令，先删除后设新地址
```

git remote rm origin 
git remote add origin [url]
```

### 直接修改配置文件

```
文件位置：git/config 
config

[core]
    repositoryformatversion = 0
    filemode = false
    bare = false
    logallrefupdates = true
    symlinks = false
    ignorecase = true
[gui]
    wmstate = normal
    geometry = 841x483+225+101 189 218
[remote "origin"]
    url = git@github.com:project.git
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```

### 补充：如果用sourcetree的话可以直接修改远程仓库地址

