---
title:   iOS开发之位移枚举和按位或按位与运算
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---



>位移枚举(可复选的枚举) 使用位移实现选项变量

### Autoresizing 的系统枚举UIViewAutoresizing 讲述

以下位移已经计算提前计算出来了二进制与十进制值为了方便下文使用

``` objectivec
typedef NS_OPTIONS(NSUInteger,UIViewAutoresizing){    二进制值    十进制

    UIViewAutoresizingNone                 =0,         00000000  0

    UIViewAutoresizingFlexibleLeftMargin   =1<<0,    00000001  1

    UIViewAutoresizingFlexibleWidth        =1<<1,    00000010  2

    UIViewAutoresizingFlexibleRightMargin  =1<<2,    00000100  4

    UIViewAutoresizingFlexibleTopMargin    =1<<3,    00001000  8

    UIViewAutoresizingFlexibleHeight       =1<<4,    00010000  16

    UIViewAutoresizingFlexibleBottomMargin=1<<5     00100000  32

};
```

使用枚举定义选项,每个选项均可启用或禁用，使用上述方式来定义枚举值,每个枚举值所对应的二进制表示中，只有1个二进制位的值是1。用“按位或操作符”可组合多个选项

用 | 来隔开

``` objectivec
aView.autoresizingMask=UIViewAutoresizingFlexibleTopMargin|
  UIViewAutoresizingFlexibleLeftMargin|  
  UIViewAutoresizingFlexibleBottomMargin|  
  UIViewAutoresizingFlexibleRightMargin;  
```

而且每一个枚举对应的逻辑都会覆盖到

实例

``` objectivec
-(void)todo:(UIViewAutoresizing)type{

    if(type==0){

        NSLog(@"UIViewAutoresizingNone");

        return;

    }
//更严谨的写法
    if(type&UIViewAutoresizingFlexibleLeftMargin ==   
    UIViewAutoresizingFlexibleLeftMargin){

        NSLog(@"UIViewAutoresizingFlexibleLeftMargin");

    }

    if(type&UIViewAutoresizingFlexibleWidth){

        NSLog(@"UIViewAutoresizingFlexibleWidth");

 

    }

    if(type&UIViewAutoresizingFlexibleRightMargin){

        NSLog(@"UIViewAutoresizingFlexibleRightMargin");

 

    }

    if(type&UIViewAutoresizingFlexibleTopMargin){

        NSLog(@"UIViewAutoresizingFlexibleTopMargin");

 

    }

    if(type&UIViewAutoresizingFlexibleHeight){

        NSLog(@"UIViewAutoresizingFlexibleHeight");

 

    }

    if(type&UIViewAutoresizingFlexibleBottomMargin){

        NSLog(@"UIViewAutoresizingFlexibleBottomMargin");

    }

}

-(void)viewDidLoad{

    [superviewDidLoad];

    // Do any additional setup after loading the view, typically from a nib.

    [self todo:UIViewAutoresizingFlexibleLeftMargin|  
    UIViewAutoresizingFlexibleRightMargin|  
    UIViewAutoresizingFlexibleHeight];  

}
```

结果输出

``` objectivec
UIViewAutoresizingFlexibleLeftMargin  
UIViewAutoresizingFlexibleRightMargin  
UIViewAutoresizingFlexibleHeight  
```

### 二进制转十进制

`1101（2）=1*2^0+0*2^1+1*2^2+1*2^3=1+0+4+8=13`转化成十进制要从右到左用二进制的每个数去乘以2的相应次方不过次方要从0开始

#### 位移位运算

如 `UIViewAutoresizingFlexibleHeight  = 1 << 4`,

1.左移运算 1 << 4
将一个运算对象的各二进制位全部左移若干位（左边的二进制位丢弃，右边补0）。

1 转化为二进制为 :0000 0001

左移四位就为     :0001 0000

0001 0000 转化为十进制等于16

2.右移运算 90>>4
将一个数的各二进制位全部右移若干位，正数左补0，负数左补1，右边丢弃。操作数每右移一位，相当于该数除以2。

90转化为二进制为 :01011010

右移4位就是          :00000101

00000101  转化为十进制等于5

#### 按位或运算符（|）

运算规则：0|0=0；   0|1=1；   1|0=1；    1|1=1；即 ：参加运算的两个二进制对应数位只要有一个为1，其值为1。

例如

``` objectivec
[self todo:UIViewAutoresizingFlexibleLeftMargin|
UIViewAutoresizingFlexibleRightMargin|  
UIViewAutoresizingFlexibleHeight];
```

1.十进制1|4|16 转为二进制0000 0001 | 0000 0100 | 0001 0000  =  0001 0101,因此，1|4|16的十进制值得21

#### 按位与运算符（&）

参加运算的两个数据，按二进制位进行“与”运算。运算规则：0&0=0;   0&1=0;    1&0=0;     1&1=1;即：两对应数位同时为“1”，结果才为“1”，否则为0

1.十进制3&5  转为二进制 0000 0011 & 0000 0101 = 0000 0001   因此，3&5的值得1

2.iOS在方法中的应用

``` objectivec
-(void)todo:(UIViewAutoresizing)type{if (type & 
UIViewAutoresizingFlexibleLeftMargin )
 {NSLog(@"UIViewAutoresizingFlexibleLeftMargin");}}

入参数type 为 UIViewAutoresizingFlexibleLeftMargin|
UIViewAutoresizingFlexibleRightMargin|
UIViewAutoresizingFlexibleHeight
```

上文知道结果是 0001 0101,十进制值得21 `UIViewAutoresizingFlexibleRightMargin为4`

0001 0101 &  `UIViewAutoresizingFlexibleRightMargin` =  0001 0101 & 0000 0100  =21&4 = 4 根据计算结果还是`UIViewAutoresizingFlexibleRightMargin`这个枚举

### 在iOS中的总结

如果把传递给某个方法的选项表示为枚举类型，而多个选项又可同时使用，那么就将各选项值定义为2的幂，以便通过按位或操作将其组合起来。

用`NS_ENUM`与`NS_OPTIONS`宏来定义枚举类型，并指明其底层数据类型。这样做可以确保枚举是用开发者所选的底层数据类型实现出来的，而不会采用编译器所选的类型。

在处理枚举类型的`switch`语句中不要实现`default`分支。这样的话，加入新枚举之后，编译器就会提示开发者：`switch`语句并未处理所有枚举。
