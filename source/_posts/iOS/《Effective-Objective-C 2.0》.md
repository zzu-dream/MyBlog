---
title:   《Effective-Objective-C 2.0》
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---
图片原地址：https://upload-images.jianshu.io/upload_images/1457495-debf9e0c37687e51.png
![图片](https://upload-images.jianshu.io/upload_images/1457495-debf9e0c37687e51.png)  
[对应简书总结](https://www.jianshu.com/p/862b064e82e0)  
[Effective-Objective-C 2.0.pdf](https://github.com/aozhimin/awesome-iOS-resource/blob/master/Books/Effective%20Objective-C%202.0%20%20%E7%BC%96%E5%86%99%E9%AB%98%E8%B4%A8%E9%87%8FiOS%E4%B8%8EOS%20X%E4%BB%A3%E7%A0%81%E7%9A%8452%E4%B8%AA%E6%9C%89%E6%95%88%E6%96%B9%E6%B3%95.pdf)  
[iOS相关书籍汇总](https://github.com/aozhimin/awesome-iOS-resource/tree/master/Books)

-----------------------
*分界线*

-----------------------

>说明：以下内容 均来自与jatstar的汇总 只做引用学习 没有商业用途 [Effective-Objective-C 2.0](https://jatstar.cn/2016/07/10/Effective-Objective-C-2-0/)

### 熟悉Objective-C

* 起源
    1. 由消息型语言鼻祖Smalltalk演化而来。是C语言的超集。
    2. 与函数式语言关键区别：消息结构的语言，运行时所执行的代码由运行环境决定(动态绑定)；函数调用的语言，由编译器决定。
    3. NSString *someString 中 someString为指向NSString 的指针。Type * 声明的对象总是被分配的堆区(heap space) 中，而绝不可能分配的栈区(stack)。
    4. 如果只需保存int float double char 等非对象类型（nonoobject type） ，使用C结构体(如CGRect)比使用OC对象性能更优，因为创建OC对象需要分配及释放堆区内存等额外开销。 
* 在类的头文件中尽量少引入其他头文件
    1. 头文件在类的头文件中，少引入头文件，使用@Class 向前声明即可。 然后在实现文件中再引入那些类的头文件。这样可以降低类之间的耦合。
    2. 无法使用向前声明的情况，如果 引入当前类遵守的某一项协议，此时把协议单独放下一个头文件中，再将其引入。
* 多用字面量语法，少用与之等价的方法。
1. 举个🌰:

``` objectivec
NSNumber *intNumber = @1;
NSNumber *floatNumber = @2.5f;

NSArray *namesArray = @[@"Jat",@"Jay",@"Vae"];
NSString *myName = namesArray[0];

NSDictionary *personData = @{@"ChineseName":@"张建宇",
@"EnglishName":@"Jat",
@"age":@"23"}
Number *myAge = personData[@"age"];

//通过字面量创建的数组或者字典 ，如果值中有nil，会抛出异常。
```
* 多用类型常量，少用＃define 预处理指令。  
    1. ＃define定义的出来的常量，不包含类型信息，编译器需要再编译前执行查找替换，会增加编译时间。  
    2. 只在当前类使用的常量，可以使用 static const 在.m中定义。  
    3. 在头文件中使用extern来声明全局变量,并在相关实现文件中定义其值。命名时，通常使用于是相关的类名最为前缀。如  UITextFieldTextDidBeginEditingNotification 。  
    4. 《iOS开发中 const,static,extern用法总结》  
* 使用枚举来表示状态，选项，状态码  
    1. 易懂的枚举名可以提高代码的可读性。  
    2. 选项为多选时，使用二进制表示枚举值，以便通过按位或将其组合起来。🌰：  UIInterfaceOrientationMask。  
    3. switch语句中，不要实现default分支。这样加入新的枚举之后，编译器会提示：switch语句没有处理所有枚举值。  
### 消息／对象／运行时

* 理解“属性” 这一概念 Objective-C语法@property详解
* 在对象内部尽量直接访问实例变量。
    1. 直接访问实例变量不经过方法派发，比点语法快。
    2. ⚠️直接访问copy修饰的属性，不会掉用setter方法，所以不会拷贝该属性。
    3. ⚠️不会触发KVO通知。是否会产生问题，视情况而定。
    4. 初始化方法和dealloc方法中，总是应该直接访问。
    5. ⚠️注意考虑懒加载的情况下，要使用点语法。
* 理解“对象等同性”这一概念。
    1. ==比较的是指针地址是否一样。
    2. 特有的等同性判断方法，如isEqualToString比isEqual快一些。
    3. 相同的对象必须具有相同的哈希码，但是哈希码相同的对象未必相同。
    4. 不必逐条比较每个属性的哈希码，依情况，使用速度快，碰撞率低的算法。
* 以“类族模式”隐藏实现细节
    1. 例如UIButton 中的 + (instancetype)buttonWithType:(UIButtonType)buttonType.
    2. 可以把实现细节隐藏在一个公共的接口后面。
* 在既有类中使用关联对象存放自定义数据
* 理解objc_msgSend 的作用
    1. Objective-c “动态绑定(dynamic binding)” 的特性使得所要调用的函数直到运行时才能确定。通过动态消息派发系统(dynamic message dicpatch system)来查出对应的方法并执行。
    2. 消息由接收者(receiver)，选择子(selecter)，以及参数构成。调用方法实际上相当于在给对象发送消息。
* 理解消息转发机制 //TODO： 待续
* 用方法调配技术调试黑盒方法 

``` objectivec
//Category
#import "NSString+Test.h"
#import <objc runtime.h="">

@implementation NSString (Test)
- (NSString*)eoc_myLowercaseString {
    NSString *lowercase = [self eoc_myLowercaseString];
    NSLog(@"%@ => %@", self, lowercase);
    return lowercase;
}
// 不会死循环，因为eoc_myLowercaseString与lowercaseString方法互换了，运行时期间eoc_myLowercaseString选择子实际上对应的原有的lowercaseString方法实现。
+ (void)load{
    Method originalMethod = class_getInstanceMethod([NSString class],@selector(lowercaseString));
    Method swappedMethod = class_getInstanceMethod([NSString class],@selector(eoc_myLowercaseString));
    method_exchangeImplementations(originalMethod, swappedMethod);
}
@end 
/* 
测试一下：
NSString *string = @"Hello World";
NSString *textString = [string lowercaseString];
Output:
Hello World => hello world
*/</objc>
```
* 理解类对象的用意 //TODO: 待续
### 接口与API设计

* 使用前缀避免命名空间冲突。
* 提供全能初始化方法
    1. 提供一个全能初始化方法，并与文档中指明，其他初始化方法均调用此方法。
    2. 全能初始化方法与超类不同时，应该重写，冲突时，应该加上抛异常机制提示。
* 实现description方法
    1. 自定义类，覆写description方法，返回的字符串，NSLog时的显示该字符串；
    2. 重写debugDescription，改变调试控制台输出信息，默认为description方法的返回值。
* 尽量使用不可变对象。
* 使用清晰而且协调的命名方式
* 为私有方法名加前缀
    1. 给私有方法名加上前缀(虽然我感觉没必要～也没见过知名开源项目有加；但是爱老婆说按规范要加)
    2. 不要使用下划线做私有方法的前缀，因为这种做法是预留给苹果的。
* 理解Objective-C错误模型
    1. 只有发生使整个应用崩溃的严重错误时，才之用异常。
    2. 不那么严重的错误，可以指派委托方法来处理错误，也可以把错误信息放在NSError里，由NSLog输出。 
* 理解NSCoding协议。
    1. 想令对象具有拷贝功能，需实现NSCoying协议；如果对象有可变版本，还需要实现NSMutableCopying协议。
    2. 浅拷贝之后的内容与原始内容指针地址相同，深拷贝之后的内容指向原始内容相关对象的一份拷贝。(深拷贝会逐个元素发送Copy消息，用拷贝得到元素创建Set);
* 通过委托与数据源协议进行对象间的通信。
    1. @property(nonatomic,weak)id<classnamedelegate> delegate</classnamedelegate> 用weak修饰，，防止循环引用(retain cycle);
* 将类的实现代码分散到便于管理的数个分类之中。//易于管理
* 总是为第三方类的分类名称增加前缀。
* 勿在分类中声明属性。
    1. 封装数据所用的全部属性都定义在主接口里。
    2. 关联对象可以解决分类不能合成实例变量的问题。//本书作者认为此方法内存管理上容易出错，不是很推荐。
* 使用“class-continuation”分类 隐藏实现细节 //就是Extension吧，匿名的分类。
* 通过协议提供匿名对象。 //隐藏返回值类型
### 内存管理

* 理解引用计数
* 以ARC简化引用计数
* 在dealloc方法中只释放引用并移除监听(KVO和Notifications)
* 编写 “异常安全代码”时留意内存管理问题(即：使用@try...@catch语法时)
* 以弱引用避免保留环(retain cycle :循环引用)
* 以“自动释放池块”降低内存峰值。
* 用“僵尸对象”调试内存管理问题。
    1. 系统在回收对象时，可以不将其真正回收，而是把它转化为僵尸对象。
    2. 系统会修改对象的isa指针，令其指向特殊的僵尸类。僵尸类能够响应所有的选择子，打印一条包含消息内容以及接收者的消息，然后终止程序。
* 不要使用retainCount。(ARC模式下，此方法废弃了)。
### block与GCD

//翻译成 块与大中枢派发也是醉了。。。
* 理解block这一概念。
    1. 语法结构： return_type (^block_name)(parameters)
    2. 默认情况下block外的变量需要在block中修改的，需要在声明时加__block修饰，但block修改其所在的类的成员变量时不需要加。
    3. 定义block时，它是分配在栈区的，所以。只在其作用域范围有效。调用copy拷贝到堆区之后可以和OC对象一样具备引用计数。由ARC去管理。
* 为常见的block类型创建typedef

``` objectivec
typedef int(^SomeBlock)(BOOL flag,int value);

//使用：
SomeBlock block = ^ (BOOL flag,int value){
    if(flag){
        return value * 5;
    }else{
        return value *10;
    }
}
```
* 使用handler block降低代码的分散程度。//如AFN中的网络请求回调
* 用block引用其所属对象时不要出现循环引用。
* 多用派发队列，少用同步锁。
    1. 派发队列可以用来表述同步语义(synchornization semantic),比使用@synchronized块和NSLock对象更简单。
    2. 使用同步和异步派发结合起来，可以实现与普通加锁一样的同步行为，而且不会阻塞执行异步派发的线程。
    3. 使用同步队列和栅栏块，可以让同步锁更加高效。
* 多用GCD,少用｀performSelector｀系列方法。

``` objectivec
SEL selector;
if(/* some condition */){
    selector = @selector(foo);
}else if(/* some other condition */){
    selector = @selector(bar);
}else{
    selector = @selecter(baz)
}
```

/*
运行时才能确定调用列哪个方法，
编译器没有办法在编译时按ARC的内存管理原则判定返回值是不是该释放，
编译器没有添加释放操作。
这将又可能导致内存泄漏
*/
* 掌握GCD和NSOperationQueue的使用时机。
    1. 运行任务之前，可以用在NSOperation对象上调用cancel取消该任务。
    2. 可以指定任务间的依赖关系。
    3. 可以通过KVO监听NSOperation的属性。例如isFinished,isCancelled。
    4. 指定操作的优先级。
    5. 重用NSOperation对象。
* 通过Dispathtch Group机制，根据系统资源状况来执行任务。
* 使用dispatch_once来执行只需运行一次的线程安全代码。

``` objectivec
+(id)sharedInstance{
    static SomeClass *sharedInstance = nil;
    static dispatch_once_t onceToken;
    dispatch_once(@onceToken,^{
        sharedInstance = [[self alloc]init];
    })
    return sharedInstance;
}
```
* 不要使用dispatch_get_current_queue(void);//调试还是可以用下的
### 系统框架

* 熟悉系统框架。
    1. CFNetWork:提供C语言级别的网络通信能力，将BSDsocket抽象成易于使用的接口。
    2. CoreAudio:提供的C语言API可用来操作设备上的音频硬件。
    3. AVFoundation:处理音频视频的录制，回放。
    4. CoreData:用于实现数据持久化。
    5. CoreText:提供C语言接口，用于执行文字排版以及渲染操作。
* 多用block枚举，少用for循环。//block枚举本身通过GCD并发执行遍历，更高效。
* 对自定义其内存管理语义的cellection使用无缝桥接。
* 构建缓存时选用NSCache而非NSDictionary.// low memory时 NSCache会自动删减缓存
* 精简initalize和load的实现代码。
    1. iOS平台上，当类或者分类载入系统时，会先调用+(void) load;同时实现时，先调类里面的，再调用分类里面的。
    2. 无法判断各个类载入的顺序，所以在load方法使用第三方类比较危险。
    3. load方法会阻塞线程，所以要尽量精简里面的代码。
    4. 首次使用某个类是，会调用该类的+(void) initalize方法，可以覆写该方法做一些与类相关的初始化操作。但是同load一样，也应该尽量精简。
* 别忘了NSTimer会保留目标对象。//weakSelf大法打破循环就好了。