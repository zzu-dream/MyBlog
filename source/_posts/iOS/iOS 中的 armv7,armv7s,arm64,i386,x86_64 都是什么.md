---
title:   OS 中的 armv7,armv7s,arm64,i386,x86_64 都是什么
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---

在做静态库的时候以及引用静态库的时候经常会遇到一些关于真机模拟器不通用的情况，会报错找不到相应库导致编译失败，

这里简单记录一下各种设备支持的架构。

 

#### iOS测试分为模拟器测试和真机测试，处理器分为32位处理器，和64位处理器

##### 模拟器

模拟器32位处理器测试需要i386架构，（iphone5,iphone5s以下的模拟器）

模拟器64位处理器测试需要x86_64架构，(iphone6以上的模拟器)

##### 真机

真机32位处理器需要armv7,或者armv7s架构，（iphone4真机/armv7,      ipnone5,iphone5s真机/armv7s）

真机64位处理器需要arm64架构。(iphone6,iphone6p以上的真机)

project -> target -> building setting -> Arhitectures 设置

##### 设置
debug属性设置为no的时候，会编译支持所有架构的版本，编译的速度会变慢，设置为yes 的时候，只编译当前的architecture版本，编译速度快。

一般情况下，debug 设置为yes，release为no，这样发行版本能适应不同设备。

##### 用到的命令行查看或者合并

静态库.a支持信息：
lipo -info .a文件  
 
两个静态库合并：
 lipo -create 文件1  文件2  -output /Users/sunjianfei/Desktop/libPrint.a