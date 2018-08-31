---
title:  git项目中的常用功能
tags:  [git删除缓存远程分支]
categories:  [git]
date:  2018-06-11 16:17:22
---


### 列出提交个数   主要用来设置项目build号
```
git rev-list --count HEAD
```

### 获得两个版本间所有变更的文件列表

```
git diff 6962e097c87bcbd937eb59d94f9f79b9a709455d   
c02e20f5ad5eb1a675b6b3d30fed5b66f309871c --stat > log.txt -p
```

### 查看某个文件的修改历史

`git log -p filePath/fileName.m `

### 使用 pull rebase 操作替代 merge

　　如果你工作的团队正工作在同一个分支，那么你所要做的获取/合并或经常拉取。分支合并的 git 记录与合并提交时提示功能分支被并入主干。但在多个团队成员工作的同一分支的情况下，经常合并导致在日志中多个合并的消息引起混乱。所以你可以使用 pull rebase，以保持历史信息清除了无用合并的消息。

`git config branch.BRANCH_NAME_HERE.rebase true`

　　此外，您可以配置一个特定的分支总是衍合：

`git pull --rebase `

### gc 命令

“垃圾回收”是一个很亲切的功能。让我们开始吧：  
`$ git gc --prune=now`  
现在，重新检视一下仓库的大小，发现确实有效啊：

```
$ find .git/objects -type f
.git/objects/info/packs
.git/objects/pack/pack-9d75315485cb7bfbf51ce5c94a4535da99b58dbb.idx
.git/objects/pack/pack-9d75315485cb7bfbf51ce5c94a4535da99b58dbb.pack
$
$ du -ah    # 此处略去了无关输出
4.0K    ./.git/objects/pack/pack-9d75315485cb7bfbf51ce5c94a4535da99b58dbb.idx
 52M    ./.git/objects/pack/pack-9d75315485cb7bfbf51ce5c94a4535da99b58dbb.pack
 77M    ./bigfile
130M    .
```

### cherry-pick用法

使用场景：在branch1开发，进行多个提交，这是切换到branch2，想把之前branch1分支提交的commit都复制过来。


单个`commit`只需要`git cherry-pick commitid`

多个`commit` 只需要`git cherry-pick commitid1..commitid100`

注意，不包含第一个`commitid` ， 即  `git cherry-pick (commitid1..commitid100]`