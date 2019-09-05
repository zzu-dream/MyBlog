---
title:  泛型
tags:  [android学习]
categories:  [android]
date:  2018-06-11 16:17:22
---



### 什么是泛型？
泛型，大概的意思是指没有指定具体的类型的类或方法，以泛型的形式传入一个类中或方法中，在Java编程(Android编程)里面使用一对尖括号和一个大写字母表示，例如：

``` java
//泛型类
public interface List<E>{}

//泛型方法，类型参数位于返回类型之前或void之前
public static <E> boolean contains(E [] arr, E x){
   for(E val:arr){
      if(x.equal(val)){
         return true;
      }
   }
   return false;
}

```
 
