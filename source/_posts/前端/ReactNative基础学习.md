
---
title: ReactNative基础学习
tags: ReactNative基础
categories: ReactNative
date:  2018-06-15 16:17:22
---

## 组件的生命周期


组件装载，组件在渲染之前，会先调用默认的props，ES6就是，static defaultProps；接下来就是组件初始化，constructor（props）组件的构造方法；接下来是 componentWillMount组件在加载之前的方法；render完成组件的渲染；componentDidMount 组件渲染完成。接下来就进入运行阶段啦。（一次调用）

组件更新，在运行中，如果组件的属性发生了改变，就会调用 componentWillReceiveProps 会被调用，然后就会调用 shouldComponentUpdate ，询问我们是否要渲染组件，如果返回FALSE的话，就不会渲染；如果是TRUE的话，就会调用componentWillUpdate重新渲染组件，然后render，再后来就完成更新啦componentDidUpdate（多次调用）

组件卸载，页面关闭的时候，组件会被卸载，componentWillUnmount，可以完成资源的回收与释放啦。（一次调用）

## 创建组件的三种方式

``` js
/*
* 方式1 ES6
* */
export default class NewView extends Component{
    render(){
        return <Text style={styles.container}>hello ES6</Text> ;
    }
}

/*
 * 方式2 ES5  需要module.exports
 * */

// var NewView = React.createClass({
//     render(){
//         return <Text style={styles.container}>hello ES5</Text> ;
//     }
// })
// module.exports = NewView;

/*
 * 方式3 函数式  需要module.exports
 * 无状态，不能使用this，但是可以传入属性
 * */

// function NewView(props) {
//     return <Text style={styles.container}>hello {props.name}</Text> ;
// }
// module.exports = NewView;

```

## 组件的导入和导出

```
一、导出组件
三种导出方式，之前学过的ES6, ES5, 函数式三种建立组件方式，里面有提及过如何导出

使用方式：
import EIComponent from './EIComponent'

二、导出变量
方法一：
export var name = 'sun';
export var age = 'female';

方法二：
var name = 'sun';
var age = '22';
export {name, age};

使用方式：
例如setup.js中加入：
import EIComponent,{name,age} from './EIComponent'

三、导出方法
方法前加export
export function sum(a,b){
    return a+b;
}

使用方式：
和变量使用方式一致
import EIComponent,{name,age,sum} from './EIComponent'

```

## React Native props使用详解

```
1、什么是props? 父组件传递给子组件的属性
2、如何使用props?
3、什么是默认属性以及它的作用？ 
4、如何对props进行约束和检查？
5、props使用小技巧之延展操作符？
6、props使用小技巧之解构赋值？

props使用技巧--延展操作符
延展操作符是ES6中的新语法。当我要传递很多个属性时，
let params = {name:'张'，age:18, sex:'女' }；
使用的时候就是 <PropsTest name={params.name} sex={params.sex} />（但这个非常的复杂，代码也会很长）
<PropsTest { ...params } />（使用 大括号里放三个点 ...，然后接着 params 就可以在下一个页面被使用了。 ）

props使用技巧--解构赋值
延展操作符是将属性全部进行赋值，但如果只想取出部分来进行赋值，就可以使用解构赋值。
let params = {name:'张'，age:18, sex:'女' }；
let {name,sex}=params;
 <PropsTest name={name} sex={sex} /> 
它比传统的方式好是它可以从一组属性中获取指定属性，而且，少了一点点代码。
```

## 什么是state

>props是不可改变，只读的。为了实现交互，就需要用到组件的state。我们将组件看为状态机，UI是各种各样的状态，并在各种各样的状态之间可以切换，只需要改变组件的state，就会重新渲染UI。
state是组件私有的，是没有办法通过其他组件传递过来的。

```
state也可以吹气球

（导入新的资源，都会报错，因此需要将包管理器关掉，再重新启动服务即可。）

如何控制state的变化呢，在文字上设置方法，
onPress={ ()=> {this.setState ({ size:this.state.size+10}); }}
 改变state的值是用 this.setState{size:90}
<Image 
style={{width:this.state.size,height:this.state.size}}  
source={require('./qiqiu.png)}
/>
上述代码就将 Image 的大小给渲染出来啦。(动态化的UI就有啦)
```

## 什么是ref

ref是什么？
ref是组件的特殊属性，组件被渲染后，指向组件的一个引用。可以通过组件的ref属性，来获取真实的组件。
因为，组件并不是真正的DOM节点，而是存在于内存中的一种数据结构，称为虚拟的DOM，只有当它真正的插入文档之后，才变为真正的DOM节点。根据React的设计，所以的DOM变动都发生在虚拟DOM上，然后再将实际的部分反映到真实的DOM上--这就是 DOM DIff，它可以提高页面性能。


## 类 class


类
ES6中引入了class（类），让javaScript的面向对象编程变得更加简单和易于理解

一、类的导入
和导入普通的组件是一样的
import Student from './Student'; 

二、类的实例化
可以在setup.js的构造函数中，如下：
this.stu= new Student("晓明"，"男", 16);

三、使用类的实例
setup.js的render里面

this.stu.getDescription()//获取实例中的方法或属性等

四、类的继承
构造方法和方法是可以重写的

