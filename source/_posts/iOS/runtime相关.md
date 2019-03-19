---
title:   iOS runtime
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---


### class 结构（方法步骤）
```
struct objc_class {
    //类本身
    Class _Nonnull isa ;
    //父类
    Class _Nullable super_class
    //类名                             
    const char * _Nonnull name                              
    long version                                            
    long info
    //类大小                                               
    long instance_size      
    //类中的变量                                
    struct objc_ivar_list * _Nullable ivars                 
    //类中的变量 
    struct objc_method_list * _Nullable * _Nullable methodLists
    //缓存，便于下次查找                   
    struct objc_cache * _Nonnull cache
    //类中的协议                       
    struct objc_protocol_list * _Nullable protocols         
} OBJC2_UNAVAILABLE;
```

### [[NSObject alloc] init]初始化步骤

```
/*
   https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/ObjCRuntimeGuide/Articles/ocrtTypeEncodings.html#//apple_ref/doc/uid/TP40008048-CH100
     
     struct objc_class {
     Class isa // 类本身 --> {isa; methodLists(alloc)(类方法)}
     
     Class super_class                                        ;
     const char *name                                         ;
     long version                                             ;
     long info                                                ;
     long instance_size                                       ;
     struct objc_ivar_list *ivars                             ;
     struct objc_method_list **methodLists  // 实例方法                  ;
     struct objc_cache *cache                                 ;
     struct objc_protocol_list *protocols                     ;
     }
     最终指向自己，形成了一个闭环， NSObject的isa 不是指向一个nil
     1 [EOCObject alloc] 先执行，因为EOCObject检测，没有alloc方法， 就去父类里面去查找。
     2 检测父类是否响应 alloc， 如果有，那么执行， 开始分配内存空间大小（成员变量）。// 方法（类有关系）
     3 init 方法，检测是否响应，如果没有去父类查找。
     4 方法执行完，会存缓存（所以一般第二次操作，会更快）
     */
    MyObject * objc  = [[MyObject alloc] init];
```

### main()之前的过程有哪些？

1`main`之前的加载过程  
1）`dyld` 开始将程序二进制文件初始化  
2）交由`ImageLoader` 读取 `image`，其中包含了我们的类，方法等各种符号`（Class、Protocol 、Selector、 IMP）`  
3）由于`runtime` 向`dyld` 绑定了回调，当`image`加载到内存后，`dyld`会通知`runtime`进行处理  
4）`runtime` 接手后调用`map_images`做解析和处理  
5）接下来`load_images` 中调用`call_load_methods`方法，遍历所有加载进来的`Class`，按继承层次依次调用Class的`+load`和其他Category的`+load`方法  
6）至此 所有的信息都被加载到内存中  
7）最后`dyld`调用真正的`main`函数  



* 对象的`isa`指针指向所属的类  
* 类的`isa`指针指向了所属的元类  
* 元类的`isa`指向了根元类，根元类指向了自己。
* 类的`superClass` 指向父类最终到根类
* 根类的`superclass`指向`nil`
* 元类的`superclass` 指向父元类，最终到根元类
* 根元类的`superclass` 指向根类


![](https://upload-images.jianshu.io/upload_images/1682758-675c67c6868038d1?imageMogr2/auto-orient/)

class_isMetaClass用于判断Class对象是否为元类，object_getClass用于获取对象的isa指针指向的对象。


### 仓库地址
[dream001 demo仓库地址](https://coding.net/u/dream001/p/iOS_runtime/git/tree/master)  
[苹果官网开源代码](https://opensource.apple.com/source/objc4/)  
[官方api](https://developer.apple.com/documentation/objectivec/objective_c_runtime#//apple_ref/doc/uid/TP40001418-CH1g-126286)

[掘金runtime实战总结]( https://juejin.im/post/5ac0a6116fb9a028de44d717   )  
[IOS程序在main函数前所做的事情](https://maxwellqi.github.io/ios-primary-main/)  [main](http://blog.sunnyxx.com/2014/08/30/objc-pre-main/)  
[devtang](http://blog.devtang.com/2014/09/09/ios-weekly-24/)


[深入理解Objective-C的Runtime机制](https://www.csdn.net/article/2015-07-06/2825133-objective-c-runtime/1)