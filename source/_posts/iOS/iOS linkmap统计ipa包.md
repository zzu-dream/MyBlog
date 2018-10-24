---
title:   iOS linkmap统计ipa包
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---



iOS APP编译后，除了一些**资源文件**，剩下的就是一个**可执行文件**，有时候项目大了，**引入的库多了，可执行文件很大**，想知道这个可执行文件的构成是怎样，里面的内容都是些什么，哪些库占用空间较高，可以用以下方法勘察：  

**1.**XCode开启编译选项`Write Link Map File`
`XCode -> Project -> Build Settings ->` 搜`map -> 把Write Link Map File`选项设为`yes`，并指定好`linkMap`的存储位置

**2.**编译后，到编译目录里找到该txt文件，文件名和路径就是上述的`Path to Link Map File`
位于`~/Library/Developer/Xcode/DerivedData/XXX-eumsvrzbvgfofvbfsoqokmjprvuh/Build/Intermediates/XXX.build/Debug-iphoneos/XXX.build/`
这个`LinkMap`里展示了整个可执行文件的全貌，列出了编译后的每一个.o目标文件的信息（包括静态链接库.a里的），以及每一个目标文件的代码段，数据段存储详情。


### 在LinkMap里首先列出来的是目标文件列表：

```
# Object files:
[ 0] linker synthesized
[ 1] /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator7.0.sdk/usr/lib/crt1.o
[ 2] /Users/bang/Library/Developer/Xcode/DerivedData/yishu-eyzgphknrrzpevagadjtwpzzeqag/Build/Intermediates/yishu.build/Debug-iphonesimulator/yishu.build/Objects-normal/i386/TKPFileInfo.o
...
[280] /Users/bang/Downloads/yishu/yishu/Classes/lib/UMeng/MobClick/libMobClickLibrary.a(UMANJob.o)
[281] /Users/bang/Downloads/yishu/yishu/Classes/lib/UMeng/MobClick/libMobClickLibrary.a(UMANWorker.o)
[282] /Users/bang/Downloads/yishu/yishu/Classes/lib/UMeng/MobClick/libMobClickLibrary.a(MobClick.o)
[283] /Users/bang/Downloads/yishu/yishu/Classes/lib/UMeng/MobClick/libMobClickLibrary.a(UMANLaunch.o)
...

```

前面中括号里的是这个文件的编号，后面会用到，像项目里引用到静态链接库libMobClickLibrary.a里的目标文件都会在这里列出来。

### 接着是一个段表，描述各个段在最后编译成的可执行文件中的偏移位置及大小，包括了代码段（__TEXT，保存程序代码段编译后的机器码）和数据段（__DATA，保存变量值）

```
# Sections:
# Address   Size     Segment   Section
0x00002740 0x00273890 __TEXT __text
0x00275FD0 0x00000ADA __TEXT __symbol_stub
0x00276AAC 0x00001222 __TEXT __stub_helper
0x00277CCE 0x00019D9E __TEXT __objc_methname
0x00291A70 0x00012847 __TEXT __cstring
0x002A42B7 0x00001FC1 __TEXT __objc_classname
0x002A6278 0x000046A7 __TEXT __objc_methtype
0x002AA920 0x000061CE __TEXT __ustring
0x002B0AF0 0x00000764 __TEXT __const
0x002B1254 0x000028B8 __TEXT __gcc_except_tab
0x002B3B0C 0x00004EBC __TEXT __unwind_info
0x002B89C8 0x0003662C __TEXT __eh_frame
0x002EF000 0x00000014 __DATA __program_vars
0x002EF014 0x00000284 __DATA __nl_symbol_ptr
0x002EF298 0x0000073C __DATA __la_symbol_ptr
0x002EF9E0 0x000030A4 __DATA __const
0x002F2A84 0x00000590 __DATA __objc_classlist
0x002F3014 0x0000000C __DATA __objc_nlclslist
0x002F3020 0x0000006C __DATA __objc_catlist
0x002F308C 0x000000D8 __DATA __objc_protolist
0x002F3164 0x00000008 __DATA __objc_imageinfo
0x002F3170 0x0002BC80 __DATA __objc_const
0x0031EDF0 0x00003A30 __DATA __objc_selrefs
0x00322820 0x00000014 __DATA __objc_protorefs
0x00322834 0x000006B8 __DATA __objc_classrefs
0x00322EEC 0x00000394 __DATA __objc_superrefs
0x00323280 0x000037C8 __DATA __objc_data
0x00326A48 0x000096D0 __DATA __cfstring
0x00330118 0x00001424 __DATA __objc_ivar
0x00331540 0x00006080 __DATA __data
0x003375C0 0x0000001C __DATA __common
0x003375E0 0x000018E8 __DATA __bss

```
首列是数据在文件的偏移位置，第二列是这一段占用大小，第三列是段类型，代码段和数据段，第四列是段名称。
每一行的数据都紧跟在上一行后面，如第二行`__symbol_stub`的地址`0x00275FD0`就是第一行`__text`的地址`0x00002740`加上大小`0x00273890`，整个可执行文件大致数据分布就是这样。
这里可以清楚看到各种类型的数据在最终可执行文件里占的比例，例如`__text`表示编译后的程序执行语句，`__data`表示已初始化的全局变量和局部静态变量，`__bss`表示未初始化的全局变量和局部静态变量，`__cstring`表示代码里的字符串常量，等等。

### 接着就是按上表顺序，列出具体的按每个文件列出每个对应字段的位置和占用空间

```
# Address Size File Name
0x00002740 0x0000003E [ 1] start
0x00002780 0x00000400 [ 2] +[TKPFileInfo parseWithDictionary:]
0x00002B80 0x00000030 [ 2] -[TKPFileInfo fileID]
...
```
同样首列是数据在文件的偏移地址，第二列是占用大小，第三列是所属文件序号，对应上述Object files列表，最后是名字。
例如第二行代表了文件序号为2（反查上面就是TKPFileInfo.o）的parseWithDictionary方法占用了1000byte大小。

### 使用
这个文件可以让你了解整个APP编译后的情况，也许从中可以发现一些异常，还可以用这个文件计算静态链接库在项目里占的大小，有时候我们在项目里链了很多第三方库，导致APP体积变大很多，我们想确切知道每个库占用了多大空间，可以给我们优化提供方向。LinkMap里有了每个目标文件每个方法每个数据的占用大小数据，所以只要写个脚本，就可以统计出每个.o最后的大小，属于一个.a静态链接库的.o加起来，就是这个库在APP里占用的空间大小。

### 生成的linkmap文件path

/Users/wenyongjun/Library/Developer/Xcode/DerivedData/JDViewKitProduct-cvqwuevthaoawvbqwonrghbfhnuz/Build/Intermediates.noindex/JDViewKitProduct.build/Debug-iphonesimulator/JDViewKitProduct.build/JDViewKitProduct-LinkMap-normal-x86_64.txt 


[基于LinkMap分析iOSAPP各模块体积](https://blog.csdn.net/zgzczzw/article/details/79855660)

[iOS APP可执行文件的组成](http://blog.cnbang.net/tech/2296/)