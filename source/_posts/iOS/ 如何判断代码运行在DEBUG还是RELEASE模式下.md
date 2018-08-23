---
title:   如何判断代码运行在DEBUG还是RELEASE模式下？
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---


>
首先确定下项目的 Build Settings 是否已经设置过宏定义 DEBUG，如何看呢？
点击 Build Settings ，然后在搜索框里输入‘macros’

![](/images/debug.png)
>如果已经设置过，在 Preprocessor Macros 的 Debug 后面会有 DEBUG=1，如果没有，就手动设置下。
接下来就可以这样做了

 ```objc
	#ifdef DEBUG
	    //do sth.
	#else
	    //do sth.
	#endif
 ```
 
>http://stackoverflow.com/a/9063682
>  
一般Apple已经为我们设置好了 DEBUG 的宏定义，所以，我们只要让 NSLog 在 DEBUG 模式下失效就好了，这样能让我们的程序运行起来更加稳定，同时我们也可以继续使用正规的 NSLog。

```objc

//put this in prefix.pch

#ifndef DEBUG
#undef NSLog
#define NSLog(args, ...)
#endif
```