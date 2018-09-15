---
title:   iOS 加载http的方法
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---

在iOS 9的时候,默认非HTTS的网络是被禁止的,我们可以在info.plist文件中添加NSAppTransportSecurity字典,将NSAllowsArbitraryLoads设置为YES来禁用ATS

[简书地址](https://www.jianshu.com/p/bee253cb4825)


解决方案一：

开启 NSAllowsArbitraryLoads 为 YES，然后提交时进行说明

解决方案二：

设置 NSExceptionDomains 属性来访问指定域名，然后提交时进行说明

解决方案三：

只针对网页浏览和视频播放的行为且为iOS 10及以上，设置NSAllowsArbitraryLoadsInWebContent为Yes。
