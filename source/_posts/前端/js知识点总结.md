
---
title: 开发前端react项目 知识点总结
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
[JavaScript 中的对象拷贝](https://www.css88.com/archives/8319)

* 使用 `Object.assign()` 方法用于将从一个或多个源对象中的所有可枚举的属性值复制到目标对象

```
let obj = {
  a: 1,
  b: 2,
};
let objCopy = Object.assign({}, obj);
console.log(objCopy);
// Result - { a: 1, b: 2 }

```
* 使用`JSON.parse(JSON.stringify(object))`

```
let obj = { 
  a: 1,
  b: { 
    c: 2,
  },
}
 
let newObj = JSON.parse(JSON.stringify(obj));
 
obj.b.c = 20;
console.log(obj); // { a: 1, b: { c: 20 } }
console.log(newObj); // { a: 1, b: { c: 2 } } (一个新的对象)
```

#### Chrome react调试插件
[React - React Developer Tools开发者工具的安装与使用（Chrome调试插件）](http://www.cnplugins.com/zhuanti/how-to-use-react-tools.html)

#### 从React15.5起，React.PropTypes被移入到单独的package中

[使用 PropTypes 进行类型检查](https://react.docschina.org/docs/typechecking-with-proptypes.html)

**需要我们安装软件包prop-types 安装方法为：**

* 安装prop-types `npm install prop-types --save`      

* 导入  `import { PropTypes} from 'prop-types';`

* 使用

```
  static defaultProps = {
    name: 'stranger'
  }
  
static propTypes = {
        autoPlay: PropTypes.bool.isRequired,
        maxLoops: PropTypes.number.isRequired,
        posterFrameSrc:PropTypes.string.isRequired,
        videoSrc: PropTypes.string.isRequired,
        nameString: PropTypes.string.isRequired,
    };  
     
```

#### CSS3的calc()使用

calc()从字面我们可以把他理解为一个函数function。其实calc是英文单词calculate(计算)的缩写，是css3的一个新增的功能，用来指定元素的长度。比如说，你可以使用calc()给元素的border、margin、pading、font-size和width等属性设置动态值。为何说是动态值呢?因为我们使用的表达式来得到的值。不过calc()最大的好处就是用在流体布局上，可以通过calc()计算得到元素的宽度。

[CSS3的calc()使用](https://www.w3cplus.com/css3/how-to-use-css3-calc-function.html)

#### 如果变量名与属性名不一致，必须写成下面这样。

```
let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
baz // "aaa"

let obj = { first: 'hello', last: 'world' };
let { first: f, last: l } = obj;
f // 'hello'
l // 'world'
```

#### ES6 引入了一种新的原始数据类型Symbol
ES6 引入了一种新的原始数据类型Symbol，表示独一无二的值。它是 JavaScript 语言的第七种数据类型，前六种是：undefined、null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。