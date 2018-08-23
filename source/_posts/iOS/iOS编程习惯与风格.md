---
title:  iOS编程习惯与风格
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2016-06-11 16:17:22
---


### 开发前
```
首先在开发前确定好需求 对需求点分析 
1、对感觉不太合理的地方 提出来或者有自己的建议 
把不合理的地方阉割在开发开始之前（做愉快编程）
2、分析接口 做开发前的进一步预判
```
### 开发中
```
1、头文件内只包含外部模块可调用的属性或者方法
2、模块构建的时候可首先按逻辑与UI交互类来区分管理（逻辑管理类、ViewController）
3、.m文件 内容实现上按区域划分（#pragma mark -来区域划分）
	（具体可为：初始化区域、自定义视图区域、自定义方法区域、生命循环区域、回调区域等）
4、视图层尽量做到封装（这样保证一个大模块都是若干小模块组合而成）
5、网络请求放到逻辑管理类中，VC中只管理数据返回后的渲染
6、抽象数据模型
7、适当添加注释（借助VVDoc）
```
>>>封装的目的代码复用，提高了代码的可维护性等

>>>在相应的模块给dealloc 打个log 看是否有内存泄露的情况

### 一些有意思的写法
```
1、- (void)xxxMethod {
  if ([xxx boolValue]) {
    //todo：xxx
  }
}

2、
if (xxx == nil) {}
if (xxx == NO) {}
if (xxx == YES) {} 


3、局部变量、实例变量、方法名  保持全名命名 不缩减 （驼峰序列）

4、（估计此处也同样会有质疑声）
if (xxx)
{
  //todo：something
}
else {
  //todo：something
}

5 、instancetype 与 id 的使用 

6、[NSNumber numberWithInt:xxx] -> @xxx 等类似的形式 
```
### 重构
```
重构？
何时重构：随时随地（事不过三）
哪些情况下就要考虑重构？
  重复代码、过长的函数、函数过多的参数列、过大的类、

把一些开发技巧编程一种习惯，更能编写高效率、高质量的代码
```

### 学习外部地址
[刘彦玮博客总结](http://liuyanwei.jumppo.com/2016/02/29/iOS-objc-styleguide.html)  
 [objc禅翻译](https://github.com/oa414/objc-zen-book-cn/)  
 [Google 开源项目风格指南 - objc](https://zh-google-styleguide.readthedocs.io/en/latest/google-objc-styleguide/contents/)