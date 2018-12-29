---
title:  Flex布局
tags:  [Flex布局]
categories: [前端]
---

#### Flex布局是什么？	

Flex是Flexible Box的缩写，意为”弹性布局”，用来为盒状模型提供最大的灵活性。
![](http://www.runoob.com/wp-content/uploads/2015/07/3791e575c48b3698be6a94ae1dbff79d.png)

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。
**项目默认沿主轴排列**。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

#### 容器的属性
以下6个属性设置在容器上。

```
flex-direction
flex-wrap
flex-flow
justify-content
align-items
align-content
```

##### flex-direction属性
flex-direction属性决定主轴的方向（即项目的排列方向）。

```
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}
```
![](http://www.runoob.com/wp-content/uploads/2015/07/0cbe5f8268121114e87d0546e53cda6e.png)

它可能有4个值。

```
row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。
```
#####  justify-content属性
justify-content属性定义了项目在主轴上的对齐方式。

```
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```
![](http://www.runoob.com/wp-content/uploads/2015/07/c55dfe8e3422458b50e985552ef13ba5.png)

5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。

```
flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
```

##### align-items属性
align-items属性定义项目在交叉轴上如何对齐。

```
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

![](http://www.runoob.com/wp-content/uploads/2015/07/2b0c39c7e7a80d5a784c8c2ca63cde17.png)

取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。

```
flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
```

[Flex布局出处](http://www.runoob.com/w3cnote/flex-grammar.html)  
[Flexbox——快速布局神器](https://www.w3cplus.com/css3/flexbox-basics.html)