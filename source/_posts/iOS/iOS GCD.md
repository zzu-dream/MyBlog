---
title:   iOS之GCD
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---

[阿里云GCD](https://www.aliyun.com/jiaocheng/topic_13551.html)

*===============关于GCD的一些好用的函数===============*

#### 一次性代码(多用于单例)

```objc
static dispatch_once_t onceToken;  
dispatch_once(&;onceToken, ^{
  NSLog(@"once"); 
}); 
```

#### 延迟执行

* perform

``` objc
//可以在运行时调用方法
- (id)performSelector:(SEL)selector
//可带一个参数
- (id)performSelector:(SEL)selector withObject:(id)object
//可带两个参数
- (id)performSelector:(SEL)selector withObject:(id)object withObject:(id)object
//可延时执行方法
- (void)performSelector:(SEL)selector withObject:(id)argument afterDelay:(NSTimeInterval)delay
//可放到另一个线程中执行
- (void)performSelector:(SEL)selector onThread:(NSThread *)thread withObject:(id)argument waitUntilDone:(BOOL)wait
- (void)performSelectorOnMainThread:(SEL)selector withObject:(id)argument waitUntilDone:(BOOL)wait
 
//延后执行方法的两种实现方式：
[self performSelector:@selector(doSomething) withObject:nil afterDelay:5.0];
```
* GCD方式

``` 
dispatch_time_t time = dispatch_time(DISPATCH_TIME_NOW, (int64_t)(5.0 * NSEC_PER_SEC));
dispatch_after(time, dispatch_get_main_queue(), ^(void){
    [self doSomething];
});
 
 
//把任务放在主线程执行的两种方式
[self performSlectorOnMainThread:@selector(doSomething) withObject:nil waitUntilDone:NO];
 
dispatch_async(dispatch_get_main_queue(), ^{
    [self doSomething];
});
```

**1、**performSelector系列方法在内存管理方面容易有疏失。它无法确定将要执行的选择子具体是什么，因而ARC编译器也就无法插入适当的内存管理方法。  
**2、**performSelector系列方法所能处理的选择子太过局限了，选择子的返回值类型及发送给方法的参数个数都受到限制。  
**3、**如果想把任务放在另一个线程上执行，那么最好不要用performSelector系列方法，而是应该把任务封装到块里，然后调用GCD的相关方法来实现。

#### 栅栏函数

关键函数`dispatch_barrier_async ` 
 
* 作用:只有当栅栏函数执行完毕后才能执行后面的函数
* 需求:使用栅栏函数规定线程执行顺序
* 注意:栅栏函数不能使用全局并发队列(否则没有意义)

```objc

 dispatch_queue_t queue = dispatch_queue_create("download", DISPATCH_QUEUE_CONCURRENT); 
    dispatch_async(queue, ^{
        for (NSInteger i = 0; i < 5; i++) {NSLog(@"task1 -- %zd -- %@", i, [NSThread currentThread]);}
    });

    dispatch_barrier_async(queue, ^{

        NSLog(@"+++++++ barrier ++++++++");

    });

    dispatch_async(queue, ^{
        for (NSInteger i = 0; i < 5; i++) {

            NSLog(@"task2 -- %zd -- %@", i, [NSThread currentThread]);

        }
    });

```

#### 迭代方法 

关键函数 `dispatch_apply`

``` objc
dispatch_apply(6, queue, ^(size_t index) { 
NSLog(@"%zd------%@",index, [NSThread currentThread]); 
}); 
```