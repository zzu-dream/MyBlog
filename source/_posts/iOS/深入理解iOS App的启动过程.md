---
title:   深入理解iOS App的启动过程
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---

[深入理解iOS App的启动过程](https://blog.csdn.net/Hello_Hwc/article/details/78317863?locationNum=9&fps=1)

## 准备知识 知道概念

### Mach-O

哪些名词指的是Mach-o ?

* Executable 可执行文件
* Dylib 动态库
* Bundle 无法被连接的动态库，只能通过dlopen()加载
* Image 指的是Executable，Dylib或者Bundle的一种，文中会多次使用Image这个名词。
* Framework 动态库和对应的头文件和资源文件的集合

Apple出品的操作系统的可执行文件格式几乎都是mach-o，iOS当然也不例外。 
mach-o可以大致的分为三部分：

* Header 头部，包含可以执行的CPU架构，比如x86,arm64
* Load commands 加载命令，包含文件的组织架构和在虚拟内存中的布局方式
* Data，数据，包含load commands中需要的各个段(segment)的数据，每一个Segment都得大小是Page的整数倍。

那么Data部分又包含哪些segment呢？绝大多数mach-o包括以下三个段（支持用户自定义Segment，但是很少使用）

* `__TEXT` 代码段，只读，包括函数，和只读的字符串，上图中类似`__TEXT`,__text的都是代码段
* `__DATA `数据段，读写，包括可读写的全局变量等，上图类似中的`__DATA`,`__data`都是数据段
* `__LINKEDIT` ` __LINKEDIT`包含了方法和变量的元数据（位置，偏移量），以及代码签名等信息。


### dyld
>dyld的全称是dynamic loader，它的作用是加载一个进程所需要的image，dyld是开源的。

### Virtual Memory
>虚拟内存是在物理内存上建立的一个逻辑地址空间，它向上（应用）提供了一个连续的逻辑地址空间，向下隐藏了物理内存的细节。 
虚拟内存使得逻辑地址可以没有实际的物理地址，也可以让多个逻辑地址对应到一个物理地址。 
虚拟内存被划分为一个个大小相同的Page（64位系统上是16KB），提高管理和读写的效率。 Page又分为只读和读写的Page。


虚拟内存是建立在物理内存和进程之间的中间层。在iOS上，当内存不足的时候，会尝试释放那些只读的Page，因为只读的Page在下次被访问的时候，可以再从磁盘读取。如果没有可用内存，会通知在后台的App（也就是在这个时候收到了memory warning），如果在这之后仍然没有可用内存，则会杀死在后台的App。

### Page fault
>在应用执行的时候，它被分配的逻辑地址空间都是可以访问的，当应用访问一个逻辑Page，而在对应的物理内存中并不存在的时候，这时候就发生了一次Page fault。当Page fault发生的时候，会中断当前的程序，在物理内存中寻找一个可用的Page，然后从磁盘中读取数据到物理内存，接着继续执行当前程序。

### Dirty Page & Clean Page

1、如果一个Page可以从磁盘上重新生成，那么这个Page称为Clean Page  
2、如果一个Page包含了进程相关信息，那么这个Page称为Dirty Page  
像代码段这种只读的Page就是Clean Page。而像数据段(_DATA)这种读写的Page，当写数据发生的时候，会触发COW(Copy on write)，也就是写时复制，Page会被标记成Dirty，同时会被复制。

## 启动过程

![](/images/app_start.jpg)
### 加载动态库
>dyld会首先读取mach-o文件的Header和load commands。 
接着就知道了这个可执行文件依赖的动态库。例如加载动态库A到内存，接着检查A所依赖的动态库，就这样的递归加载，直到所有的动态库加载完毕。通常一个App所依赖的动态库在100-400个左右，其中大多数都是系统的动态库，它们会被缓存到dyld shared cache，这样读取的效率会很高。


### Rebase && Bind
为什么要Rebase？

有两种主要的技术来保证应用的安全：ASLR和Code Sign。

ASLR的全称是Address space layout randomization，翻译过来就是“地址空间布局随机化”。App被启动的时候，程序会被影射到逻辑的地址空间，这个逻辑的地址空间有一个起始地址，而ASLR技术使得这个起始地址是随机的。如果是固定的，那么黑客很容易就可以由起始地址+偏移量找到函数的地址。

* Rebase 修正内部(指向当前mach-o文件)的指针指向
* Bind 修正外部指针指向

### Objective C

Objective C是动态语言，所以在执行main函数之前，需要把类的信息注册到一个全局的Table中。同时，Objective C支持Category，在初始化的时候，也会把Category中的方法注册到对应的类中，同时会唯一Selector，这也是为什么当你的Cagegory实现了类中同名的方法后，类中的方法会被覆盖。

另外，由于iOS开发时基于Cocoa Touch的，所以绝大多数的类起始都是系统类，所以大多数的Runtime初始化起始在Rebase和Bind中已经完成。


### Initializers

接下来就是必要的初始化部分了，主要包括几部分：

+load方法。
C／C++静态初始化对象和标记为__attribute__(constructor)的方法
这里要提一点的就是，+load方法已经被弃用了，如果你用Swift开发，你会发现根本无法去写这样一个方法，官方的建议是实用initialize。区别就是，load是在类装载的时候执行，而initialize是在类第一次收到message前调用。


### Main函数之后
从main函数开始执行，到你的第一个界面显示，这期间一般会做哪些事情。

* 执行AppDelegate的代理方法，主要是didFinishLaunchingWithOptions
* 初始化Window，初始化基础的ViewController结构(一般是UINavigationController+UITabViewController)
* 获取数据(Local DB／Network)，展示给用户。

## 总结

不同的App在启动的时候做的事情往往不同，但是优化起来的核心思想无非就两个：

能延迟执行的就延迟执行。比如SDK的初始化，界面的创建。
不能延迟执行的，尽量放到后台执行。比如数据读取，原始JSON数据转对象，日志发送。
Main函数之前

Main函数之前是iOS系统的工作，所以这部分的优化往往更具有通用性。

### dylibs

启动的第一步是加载动态库，加载系统的动态库使很快的，因为可以缓存，而加载内嵌的动态库速度较慢。所以，提高这一步的效率的关键是：减少动态库的数量。

合并动态库，比如公司内部由私有Pod建立了如下动态库：XXTableView, XXHUD, XXLabel，强烈建议合并成一个XXUIKit来提高加载速度。
### Rebase & Bind & Objective C Runtime

Rebase和Bind都是为了解决指针引用的问题。对于Objective C开发来说，主要的时间消耗在Class/Method的符号加载上，所以常见的优化方案是：

减少__DATA段中的指针数量。
合并Category和功能类似的类。比如：UIView+Frame,UIView+AutoLayout…合并为一个
删除无用的方法和类。
多用Swift Structs，因为Swfit Structs是静态分发的。感兴趣的同学可以看看我之前这篇文章：《Swift进阶之内存模型和方法调度》
### Initializers

通常，我们会在+load方法中进行method-swizzling，这也是Nshipster推荐的方式。

用initialize替代load。不少同学喜欢用method-swizzling来实现AOP去做日志统计等内容，强烈建议改为在initialize进行初始化。
减少__atribute__((constructor))的使用，而是在第一次访问的时候才用dispatch_once等方式初始化。
不要创建线程
使用Swfit重写代码。
