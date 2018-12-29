---
title:  redux
tags:  [react redux]
categories: [前端]
---

#### 动机

随着 JavaScript 单页应用开发日趋复杂，**JavaScript 需要管理比任何时候都要多的 state （状态）**。 这些 state 可能包括服务器响应、缓存数据、本地生成尚未持久化到服务器的数据，也包括 UI 状态，如激活的路由，被选中的标签，是否显示加载动效或者分页器等等。


[Redux 中文文档](https://www.redux.org.cn/)

### 几个关键库

```
   "react-redux": "^5.1.0",
    "redux": "^4.0.1",
    "redux-logger": "^3.0.6",
    "redux-thunk": "^2.3.0"
```    

### action内的type取名一定需要唯一的 如果多出添加重名的type 多处reducer都会收到该type的事件

所有的 reducer 都会收到 action。
reducer 通过 action.type 来进行判定处理。
如果某个 reducer 不处理某个动作，也就是没有处理这个 action.type 的 case， 就会走 default 分支，把 state 原样返回。
	

[react-redux中多个action和reducer是如何关联的](https://segmentfault.com/q/1010000012086401/a-1020000012111603)