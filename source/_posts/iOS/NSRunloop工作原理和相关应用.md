---
title:   NSRunloop工作原理和相关应用
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---
### NSRunloop与程序运行

　　　那么具体什么是NSRunLoop呢?其实NSRunLoop的本质是一个消息机制的处理模式。让我们首先来看一下程序的入口——main.m文件，一个ios程序启动后，只有短短的十行代码居然能保持整个应用程序一直运行而没有退出，是不是有点意思？程序之所以没有直接退出是因为UIApplicationMain这个函数内部默认启动了一个跟主线程相关的NSRunloop对象，而UIApplicationMain这个函数一直执行没有返回就保存程序一直运行的状态。

```
#import <UIKit/UIKit.h>

#import "AppDelegate.h"

int main(int argc, char * argv[]) {

    @autoreleasepool {

        return UIApplicationMain(argc, argv, nil, NSStringFromClass([AppDelegate class]));

    }

}
```
 

　　文章之初我们暂且将NSRunloop理解为实现这样功能的一段代码 , 这可以帮助我们更好的理解NSRunloop处理事件的过程(实际上远比这复杂的多：）)。

```
int main(int argc, char * argv[]) {

  BOOL runnning =YES;
   do{
        ...
       //处理各种操作 各种事件
       ...
      }while(running);
  
    return 0;
}
```

下面用官方提供的一幅非常经典的图片，来认识NSRunloop循环处理时间的流程。

![](http://www.cocoachina.com/cms/uploads/allimg/120703/4064_120703135151_1.png)  
通过所有的“消息”都被添加到了`NSRunLoop`中去，而在这里这些消息并分为`input source`和`Timer source` 并在循环中检查是不是有事件需要发生，如果需要那么就调用相应的函数处理。由此形成了运行->检测->休眠 ->运行 的循环状态。


[NSRunloop工作原理和相关应用](https://www.cnblogs.com/ruihaha/p/5813819.html)