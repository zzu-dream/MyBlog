---
title:  ssh
tags:  [ssh]
categories:  [git]
date:  2018-06-11 16:17:22
---

### SSH

你拥有了一个 GitHub 账号之后，就可以自由的 clone 或者下载其他项目，也可以创建自己的项目，但是你没法提交代码。仔细想想也知道，肯定不可能随意就能提交代码的，如果随意可以提交代码，那么 GitHub 上的项目岂不乱了套了，所以提交代码之前一定是需要某种授权的，而 GitHub 上一般都是基于 SSH 授权的。
那么什么是 SSH 呢？ 简单点说，SSH是一种网络协议，用于计算机之间的加密登录。目前是每一台 Linux 电脑的标准配置。而大多数 Git 服务器都会选择使用 SSH 公钥来进行授权，所以想要在 GitHub 提交代码的第一步就是要先添加 SSH key 配置。
### 生成SSH key

Linux 与 Mac 都是默认安装了 SSH ，而 Windows 系统安装了 Git Bash 应该也是带了 SSH 的。大家可以在终端（win下在 Git Bash 里）输入 ssh 检测是否已安装。

紧接着输入 `ssh-keygen -t rsa` 或者`（ssh-keygen -t rsa -C “邮箱名"）` ，什么意思呢？就是指定 rsa 算法生成密钥，接着连续三个回车键（不需要输入密码），然后就会生成两个文件 `id_rsa` 和 `id_rsa.pub` ，而 `id_rsa` 是密钥，`id_rsa.pub` 就是公钥。这两文件默认分别在如下目录里生成：
`Linux/Mac` 系统 在` ~/.ssh` 下，win系统在 `/c/Documents and Settings/username/.ssh` 下，都是隐藏文件，相信你们有办法查看的。
接下来要做的是把 `id_rsa.pub `的内容添加到 GitHub 上，这样你本地的 `id_rsa` 密钥跟 GitHub 上的 `id_rsa.pub` 公钥进行配对，授权成功才可以提交代码。
### GitHub 上添加 SSH key

第一步先在 GitHub 上的设置页面，点击最左侧 SSH and GPG keys ：

### 怎么查看 id_rsa.pub 文件的内容？
Linux/Mac 用户执行以下命令：
cd ~/.ssh
cat id_rsa.pub

### 测试是否ok

SSH key 添加成功之后，输入 ssh -T git@github.com 进行测试


[ssh向GITHUB 提交代码](http://stormzhang.com/github/2016/06/04/learn-github-from-zero4/)