
---
title: React DnD 的使用
tags: React
categories: React
date:  2018-10-30 14:17:22
---

### 核心API
想要灵活使用，就先知道几个核心API

* **DragSource** 用于包装你需要拖动的组件，使组件能够被拖拽（make it draggable）
* **DropTarget** 用于包装接收拖拽元素的组件，使组件能够放置（dropped on it）
* **DragDropContex** 用于包装拖拽根组件，`DragSource` 和 `DropTarget` 都需要包裹在`DragDropContex`内
* **DragDropContextProvider** 与 `DragDropContex 类似`，用 `DragDropContextProvider` 元素包裹拖拽根组件。

### 外部优秀网站
[React DnD 的使用](https://segmentfault.com/a/1190000014723549)  
[Drag and Drop for React](http://react-dnd.github.io/react-dnd/)  
