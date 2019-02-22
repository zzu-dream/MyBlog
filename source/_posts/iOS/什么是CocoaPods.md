---
title:  什么是cocoapods
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2016-06-11 16:17:22
---


## 产生背景
### 什么是CocoaPods

```
CocoaPods是一个用来帮助我们管理第三方依赖库的工具。
它可以解决库与库之间的依赖关系，下载库的源代码，
同时通过创建一个Xcode的workspace来将这些第三方库和我们的工程连接起来，
供我们开发使用。
使用CocoaPods的目的是让我们能自动化的、集中的、直观的管理第三方开源库。
```

### 为什么需要CocoaPods

```
   在进行iOS开发的时候，总免不了使用第三方的开源库，
比如SBJson、AFNetworking、Reachability等等。使用这些库的时候通常需要：
   下载开源库的源代码并引入工程
   向工程中添加开源库使用到的framework
   解决开源库和开源库以及开源库和工程之间的依赖关系、
   检查重复添加的framework等问题
	如果开源库有更新的时候，还需要将工程中使用的开源库删除，
重新执行前面的三个步骤
```
	
### CocoaPods的安装
```
	1、安装
	CocoaPods是用Ruby实现的，要想使用它首先需要有Ruby的环境。
	幸运的是OS X系统默认的已经可以运行Ruby了，因此我们只需要执行以下命令：
	 $ sudo gem install cocoapods  
	CocoaPods是以Ruby gem包的形式被安装的。在安装执行的过程中，
	可能会问我们是不是更新rake，输入y即可。这是因为rake gem包会在安装的过程中检查更细，
	如果有可用的新版本就会出现刚才的选项。
	在安装进程结束的时候，执行命令：
   	 $ pod setup  

   	 2、安装过程中可能遇到的问题
   	   执行完install命令半天没反应  ---被墙了
   	   gem版本过老 ---- sudo gem update --system  
   	   安装完成后，执行pod setup命令时报错：rvm use ruby-1.9.3-p448  
     3、升级CocoaPods
     	sudo gem install cocoapods  
CocoaPods的使用：
	1、创建Podfile  cd到项目目录 touch Podfile
	2、编辑Podfile 
	3、开始安装 pod install
```	

安装完成后就可以使用了

## 安装问题

### 使用cocoapods出现ld: symbol(s) not found for architecture x86_64问题
[解决方案](https://cn.aliyun.com/jiaocheng/398823.html)

## cocoapods版本兼容问题

[使用bundle管理多版本Cocoapods之间的协助开发](https://blog.csdn.net/u013749108/article/details/53239557)