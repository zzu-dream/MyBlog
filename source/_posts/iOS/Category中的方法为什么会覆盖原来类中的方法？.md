---
title:   Category中的方法为什么会覆盖原来类中的方法？
tags:  [iOS-WIKI]
categories:  [iOS]
date:  2018-06-11 16:17:22
---
### 深入了解`Category`

我们都知道`OC`代码执行时会先转成`C\C++`代码，`OC`对象转成对应的结构体；
`Category`对应的结构体我们可以通过将分类的`.m文件转成c++`文件查看：
`xcrun -sdk iphoneos clang -arch arm64 -rewrite-objc xxxxx.m`
即可生成对应的`.cpp`文件；
在`.cpp`文件中搜索`Category_t`可以看到`Category`对应的结构体：

```
struct _category_t {
const char *name;
struct _class_t *cls;
const struct _method_list_t *instance_methods;
const struct _method_list_t *class_methods;
const struct _protocol_list_t *protocols;
const struct _prop_list_t *properties;
};
```
通过观察结构体我们可以发现分类对应的结构体中有存储实例方法的列表、存储类方法的列表、存储协议的和属性的列表。


```
通过源码分析可知：系统是在运行时将分类中对应的实例方法、类方法等插入到了原来类或元类的方法列表中，且是在列表的前 
边！所以，方法调用时通过isa去对应的类或元类的列表中查找对应的方法时先查到的是分类中的方法！查到后就直接调用不在继
续查找。这即是’覆盖’的本质！

```

### 存在多个分类，调用谁？

```
当有多个分类时，会调用哪个分类中的方法呢？

这个是与编译顺序有关，最后编译的分类中对应的信息会在整合在类或元类对应列表的最前边。所以是调用最后编译的分类中的
方法！可以查看Build Phases ->Complie Source 中的编译顺序！
```


[Category中的方法为什么会覆盖原来类中的方法？](https://www.jianshu.com/p/dd57c39a5e4c)