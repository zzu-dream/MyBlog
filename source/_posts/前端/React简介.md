
---
title: React简介
tags: React
categories: React
date:  2018-06-15 16:17:22
---
#React简介
http://www.jianshu.com/p/1606f8bd46ed

## 背景介绍

>Facebook认为MVC无法满足他们的扩展需求，由于他们非常巨大的代码库和庞大的组织，使得MVC很快变得非常复复杂，每当需要添加一项新的功能或特性时，系统的复杂度就成级数增长，致使代码变得脆弱和不可预测，结果导致他们的MVC正在土崩瓦解。认为MVC不适合大规模应用，当系统中有很多的模型和相应的视图时，其复杂度就会迅速扩大，非常难以理解和调试，特别是模型和视图间可能存在的双向数据流动。


## React特点

>1、作为UI
 React可以作为MVC中的View层进行使用，并且在已有项目中很容易使用React开发新功能。
2、虚拟dom
Virtual DOM 虚拟DOM 
传统的web应用，操作DOM一般是直接更新操作的，但是我们知道DOM更新通常是比较昂贵的。而React为了尽可能减少对DOM的操作，提供了一种不同的而又强大的方式来更新DOM，代替直接的DOM操作。就是Virtual DOM,一个轻量级的虚拟的DOM，就是React抽象出来的一个对象，描述dom应该什么样子的，应该如何呈现。通过这个Virtual DOM去更新真实的DOM，由这个Virtual DOM管理真实DOM的更新。
>
>为什么通过这多一层的Virtual DOM操作就能更快呢？ 这是因为React有个diff算法，更新Virtual DOM并不保证马上影响真实的DOM，React会等到事件循环结束，然后利用这个diff算法，通过当前新的dom表述与之前的作比较，计算出最小的步骤更新真实的DOM。
3、组件化
Components 组件 
在DOM树上的节点被称为元素，在这里则不同，Virtual DOM上称为commponent。Virtual DOM的节点就是一个完整抽象的组件，它是由commponents组成。
>
>component 的使用在 React 里极为重要, 因为 components 的存在让计算 DOM diff 更高效。


## 学习准备
```
1、前端基础知识：html、css、JavaScript
2、jsx语法知识
3、es6 相关知识
```
## React和ReactNative关系

>react用于web应用开发，rn采用React方式进行移动应用开发。
rn采用React语法，用于进行JavaScript跨终端应用开发，即拥有原生native的交互体验，又能够保留React自由的开发效率，使用灵活的的html和css布局，使用React语法结构组件，然后同时运行在ios和android平台上。
