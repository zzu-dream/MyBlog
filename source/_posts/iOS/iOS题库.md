阿里、字节：一套高效的iOS面试题


[一套高效的iOS面试题](https://mp.weixin.qq.com/s/MfIYO239_BtuTPGYbzyYRA)
## 简述

笔者最近收集梳理了一些iOS相关的问题，其中大部分都是大厂面试或者面试其他人用到的，能命中大部分的面试和日常工作，更希望你可以用它来检验自己
由于问题量太大，本文只是给了问题，希望发挥圈友的动手能力，自己去探索下，也可以在下方进行评论回复你的答案或者提出更高质量的问题！！！

## runtime相关问题

runtime是iOS开发最核心的知识了，如果下面的问题都解决了，那么对runtime的理解已经很深了。
runtime已经开源了，这有一份别人调试好可运行的源码objc-runtime，也可以去官网找objc4

objc-runtime地址：https://github.com/RetVal/objc-runtime

objc4地址：https://opensource.apple.com/tarballs/objc4/

### 结构模型

介绍下runtime的内存模型（isa、对象、类、metaclass、结构体的存储信息等）
为什么要设计metaclass
class_copyIvarList & class_copyPropertyList区别
class_rw_t 和 class_ro_t 的区别
category如何被加载的,两个category的load方法的加载顺序，两个category的同名方法的加载顺序
category & extension区别，能给NSObject添加Extension吗，结果如何
消息转发机制，消息转发机制和其他语言的消息机制优劣对比
在方法调用的时候，方法查询-&gt; 动态解析-&gt; 消息转发 之前做了什么
IMP、SEL、Method的区别和使用场景
load、initialize方法的区别什么？在继承关系中他们有什么区别
说说消息转发机制的优劣
### 内存管理

weak的实现原理？SideTable的结构是什么样的
关联对象的应用？系统如何实现关联对象的
关联对象的如何进行内存管理的？关联对象如何实现weak属性
Autoreleasepool的原理？所使用的的数据结构是什么
ARC的实现原理？ARC下对retain &amp; release做了哪些优化
ARC下哪些情况会造成内存泄漏
### 其他

Method Swizzle注意事项
属性修饰符atomic的内部实现是怎么样的?能保证线程安全吗
iOS 中内省的几个方法有哪些？内部实现原理是什么
class、objc_getClass、object_getclass 方法有什么区别?
## NSNotification相关

苹果并没有开源相关代码，但是可以读下GNUStep的源码，基本上实现方式很具有参考性

GNUStep地址：https://github.com/gnustep/libs-base

实现原理（结构设计、通知如何存储的、name&amp;observer&amp;SEL之间的关系等）
通知的发送时同步的，还是异步的
NSNotificationCenter接受消息和发送消息是在一个线程里吗？如何异步发送消息
NSNotificationQueue是异步还是同步发送？在哪个线程响应
NSNotificationQueue和runloop的关系
如何保证通知接收的线程在主线程
页面销毁时不移除通知会崩溃吗
多次添加同一个通知会是什么结果？多次移除通知呢
下面的方式能接收到通知吗？为什么
1// 发送通知
2[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(handleNotification:) name:@"TestNotification" object:@1];
3// 接收通知
4[NSNotificationCenter.defaultCenter postNotificationName:@"TestNotification" object:nil];
## Runloop & KVO

### runloop

runloop对于一个标准的iOS开发来说都不陌生，应该说熟悉runloop是标配，下面就随便列几个典型问题吧

app如何接收到触摸事件的
为什么只有主线程的runloop是开启的
为什么只在主线程刷新UI
PerformSelector和runloop的关系
如何使线程保活
### KVO

同runloop一样，这也是标配的知识点了，同样列出几个典型问题

实现原理
如何手动关闭kvo
通过KVC修改属性会触发KVO么
哪些情况下使用kvo会崩溃，怎么防护崩溃
kvo的优缺点
## Block

block的内部实现，结构体是什么样的
block是类吗，有哪些类型
一个int变量被 __block 修饰与否的区别？block的变量截获
block在修改NSMutableArray，需不需要添加__block
怎么进行内存管理的
block可以用strong修饰吗
解决循环引用时为什么要用__strong、__weak修饰
block发生copy时机
Block访问对象类型的auto变量时，在ARC和MRC下有什么区别
## 多线程

主要以GCD为主

iOS开发中有多少类型的线程？分别对比
GCD有哪些队列，默认提供哪些队列
GCD有哪些方法api
GCD主线程 & 主队列的关系
如何实现同步，有多少方式就说多少
dispatch_once实现原理
什么情况下会死锁
有哪些类型的线程锁，分别介绍下作用和使用场景
NSOperationQueue中的maxConcurrentOperationCount默认值
NSTimer、CADisplayLink、dispatch_source_t 的优劣
## 视图&图像相关

AutoLayout的原理，性能如何
UIView &amp; CALayer的区别
事件响应链
drawrect &amp; layoutsubviews调用时机
UI的刷新原理
隐式动画 & 显示动画区别
什么是离屏渲染
imageName &  imageWithContentsOfFile区别
多个相同的图片，会重复加载吗
图片是什么时候解码的，如何优化
图片渲染怎么优化
如果GPU的刷新率超过了iOS屏幕60Hz刷新率是什么现象，怎么解决
## 性能优化

如何做启动优化，如何监控
如何做卡顿优化，如何监控
如何做耗电优化，如何监控
如何做网络优化，如何监控
## 开发证书

苹果使用证书的目的是什么
AppStore安装app时的认证流程
开发者怎么在debug模式下把app安装到设备呢
## 架构设计

### 典型源码的学习

只是列出一些iOS比较核心的开源库，这些库包含了很多高质量的思想，源码学习的时候一定要关注每个框架解决的核心问题是什么，还有它们的优缺点，这样才能算真正理解和吸收

AFN
SDWebImage
JSPatch、Aspects(虽然一个不可用、另一个不维护，但是这两个库都很精炼巧妙，很适合学习)
Weex/RN, 笔者认为这种前端和客户端紧密联系的库是必须要知道其原理的
CTMediator、其他router库，这些都是常见的路由库，开发中基本上都会用到
请圈友们在评论下面补充吧
### 架构设计

手动埋点、自动化埋点、可视化埋点
MVC、MVP、MVVM设计模式
常见的设计模式
单例的弊端
常见的路由方案，以及优缺点对比
如果保证项目的稳定性
设计一个图片缓存框架(LRU)
如何设计一个git diff
设计一个线程池？画出你的架构图
你的app架构是什么，有什么优缺点、为什么这么做、怎么改进
## 其他问题

PerformSelector &amp; NSInvocation优劣对比
oc怎么实现多继承？怎么面向切面（可以参考Aspects深度解析-iOS面向切面编程）
哪些bug会导致崩溃，如何防护崩溃
怎么监控崩溃
app的启动过程（考察LLVM编译过程、静态链接、动态链接、runtime初始化）
沙盒目录的每个文件夹划分的作用
简述下match-o文件结构
## 系统基础知识

进程和线程的区别
HTTPS的握手过程
什么是中间人攻击？怎么预防
TCP的握手过程？为什么进行三次握手，四次挥手
堆和栈区的区别？谁的占用内存空间大
加密算法：对称加密算法和非对称加密算法区别
常见的对称加密和非对称加密算法有哪些
MD5、Sha1、Sha256区别
charles抓包过程？不使用charles，4G网络如何抓包
## 数据结构与算法

对于移动开发者来说，一般不会遇到非常难的算法，大多以数据结构为主，笔者列出一些必会的算法，当然有时间了可以去LeetCode上刷刷题

LeetCode地址：https://leetcode.com/

八大排序算法
栈&队列
字符串处理
链表
二叉树相关操作
深搜广搜
基本的动态规划题、贪心算法、二分查找
## 总结

这些都是笔者收集的加上自身面试的一些经验总结，后期会持续收集补充，欢迎圈内的高手补充你的答案或者高质量问题

准备面试是一方面，对于非面试的iOS开发者来说更适用于检验自己，发起进阶之路。另外知识点是琐碎的，但是真的能全部弄懂并把琐碎的知识点融会贯通，构建起自己的知识体系，你就进阶一层。

