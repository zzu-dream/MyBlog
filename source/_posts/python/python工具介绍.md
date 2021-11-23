---
title:  python工具介绍
tags:  [Python3-WIKI]
categories:  [Python]
date:  2020-03-09 
---


## 视频学习
[python教程2019版](https://www.bilibili.com/video/av75855831?from=search&seid=5506272193310743526)  


```

TABLE OF CONTENT

00:00:00 Introduction
00:01:49 Installing Python 3
00:06:10 Your First Python Program
00:08:11 How Python Code Gets Executed 
00:11:24 How Long It Takes To Learn Python 
00:13:03 Variables
00:18:21 Receiving Input
00:22:16 Python Cheat Sheet
00:22:46 Type Conversion
00:29:31 Strings
00:37:36 Formatted Strings
00:40:50 String Methods
00:48:33 Arithmetic Operations
00:51:33 Operator Precedence
00:55:04 Math Functions
00:58:17 If Statements
01:06:32 Logical Operators
01:11:25 Comparison Operators
01:16:17 Weight Converter Program 
01:20:43 While Loops
01:24:07 Building a Guessing Game
01:30:51 Building the Car Game
01:41:48 For Loops
01:47:46 Nested Loops
01:55:50 Lists
02:01:45 2D Lists
02:05:11 My Complete Python Course 
02:06:00 List Methods
02:13:25 Tuples
02:15:34 Unpacking
02:18:21 Dictionaries
02:26:21 Emoji Converter
02:30:31 Functions
02:35:21 Parameters
02:39:24 Keyword Arguments 
02:44:45 Return Statement
02:48:55 Creating a Reusable Function 
02:53:42 Exceptions
02:59:14 Comments
03:01:46 Classes
03:07:46 Constructors
03:14:41 Inheritance
03:19:33 Modules
03:30:12 Packages
03:36:22 Generating Random Values
03:44:37 Working with Directories 
03:50:47 Pypi and Pip
03:55:34 Project 1: Automation with Python
04:10:22 Project 2: Machine Learning with Python 
04:58:37 Project 3: Building a Website with Django 
```

## 安装和切换python3
[mac下 将python2.7改为python3](https://www.cnblogs.com/cynthia-wuqian/p/9303514.html)

执行  
bash 环境： `source ~/.bashrc`

zsh 环境： `source ~/.zshrc`




## pyenv

Mac系统自带的Python是2.7.10，自己需要Python 3.x,此时需要在系统中安装多个Python，但又不能影响系统自带的Python,即需要实现Python的多版本共存,pyenv就是这样一个Python版本管理器 。  
[Mac安装pyenv及pyenv的使用](https://www.cnblogs.com/kumufengchun/p/10986498.html)  
1.查看pyenv安装的版本
`pyenv versions`  
2.  后边括号中内容表示这个版本是由哪条途径激活的（global、local、shell）  
`pyenv global <version>`  # 全局设置python版本为指定版本，设置全局的 Python 版本，通过将版本号写入 ~/.pyenv/version 文件的方式。  
`pyenv local <version>`   # 设置当前路径下python版本为指定版本，设置 Python 本地版本，通过将版本号写入当前目录下的 .python-version 文件的方式。<br>通过这种方式设置的 Python 版本优先级较 global 高。  
`pyenv shell <version>`   # 设置当前shell窗口使用的python版本为指定版本，设置面向 shell 的 Python 版本，通过设置当前 shell 的 PYENV_VERSION 环境变量的方式。<br>这个版本的优先级比 local 和 global 都要高。–unset 参数可以用于取消当前 shell 设定的版本。  
3.查看当前的python 版本
`pyenv version`

4.切换版本  
[root@localhost ~]# `pyenv global 3.6.4`  
[root@localhost ~]# `pyenv version`  
3.6.4 (set by /root/.pyenv/version)  


**安装的zsh遇到问题**
zsh: command not found: pyenv
[解决路径](https://www.jianshu.com/p/3e93311fe6cb)

## Anaconda

## Django
Django是一个开放源代码的Web应用框架，由Python写成。采用了MTV的框架模式，即模型M，模板T和视图V，重点就是基于Python并且是一个大而全的Web应用框架，什么都替你考虑好了.  
[Mac下Django学习](https://www.jianshu.com/p/b019496ccbee)


