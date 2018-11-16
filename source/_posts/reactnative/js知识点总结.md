
---
title: js知识点总结
tags: 前端
categories: 前端
date:  2018-06-15 16:17:22
---


#### js中的||和&&
* 逻辑与&&和逻辑或||操作符可以应用于任何类型的操作数，而不仅仅是布尔值。

* 几乎所有语言中||和&&都遵循“短路”原理， 如&&中第一个表达式为假就不会去处理第二个表达式，而||正好相反。js同样也遵循上述原则： 
　　
* 当逻辑或||时，找到为true的分项就停止处理，并返回该分项的值，否则执行完，并返回最后分项的值。
* 当逻辑与&&时，找到为false的分项就停止处理，并返回该分项的值。

``` javascript
var a = "" || null || 3 || 4;//3
alert(a);
var b = 4 && 5 && null && "0";//null
alert(b);

```

#### 扩展运算符  ... 的使用

[妙用ES6解构和扩展运算符让你的代码更优雅](https://www.cnblogs.com/chrischjh/p/4848934.html)

#### 箭头函数

[ES6箭头函数（Arrow Functions）](https://www.cnblogs.com/snandy/p/4403111.html)

####  字典合并 利用扩展运算符

```
    const obj1 = {'name': '张三', 'age': '12', 'salary': '2332'};
    const obj2 = {'fat': 'true', 'name': '李四'};

    const obj3 = {...obj1,...obj2};
    console.log('obj3=====', obj3);
    
```

#### 原生JS实现深拷贝

[原生JS实现深拷贝](https://blog.csdn.net/wang839305939/article/details/80819132)

#### React Developer Tools
[React - React Developer Tools开发者工具的安装与使用（Chrome调试插件）](http://www.cnplugins.com/zhuanti/how-to-use-react-tools.html)