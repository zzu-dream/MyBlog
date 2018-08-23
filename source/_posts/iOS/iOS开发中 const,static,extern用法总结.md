---
title:   iOS开发中 const,static,extern用法总结
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---


>iOS开发中怎么使用const,static,extern3个关键字.

### const

const的作用: const 是一个左结合的类型修饰符，它与其左侧的类型修饰符一起为一个类型修饰符,表示该类型只读.


``` objc
	修饰基本变量
	// 这两种写法是一样的，const只修饰右边的基本变量b
    const int b = 20; // b:只读变量
    int const b = 20; // b:只读变量

	修饰指针变量
	// 两种方式一样
  const int *p1; // *p1：只读 p1:只读
  int const *p1; // *p1：只读 p1:只读
  
  // const修饰指针变量p1
  int * const p1; // *p1:变量 p1:常量
  
  
  // 第一个const修饰*p1 第二个const修饰 p1
  // 两种方式一样
  const int * const p1; // *p1：常量 p1：常量
  int const * const p1;  // *p1：常量 p1：常量
```

  
简言之:沿着*号划一条线，如果const位于*的左侧，则const就是用来修饰指针所指向的变量，即指针指向为常量；如果const位于*的右侧，const就是修饰指针本身，即指针本身是常量。

### static

static的作用:

修饰局部变量：
延长局部变量的生命周期。
局部变量只会生成一份内存,只会初始化一次。
修饰全局变量:
使其只能在本文件中访问。

### extern

extern的作用: 声明和捕捉外部全局变量。
联合使用
static与const:声明一个静态的全局只读变量,(仅当前文件可访问且只读).

``` objc
static  NSString * const key = @"name";
```

extern与const组合:定义全局只读变量，多个文件共享。

``` objc
.h文件
extern  NSString * const king;
.m文件
NSString  * const king = @"king"
```

[来源const-static-extern](https://jatstar.cn/2016/01/10/const-static-extern/)


