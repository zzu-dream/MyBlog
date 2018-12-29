
---
title: hashHistory 和 browserHistory 的区别
tags: React
categories: React
date:  2018-10-30 14:17:22
---
### router的使用

* 安装
 `npm install react-router-dom --save`
* 导入
`import { HashRouter, Route, Switch, withRouter,BrowserRouter } from 'react-router-dom';`

* 官方推荐使用browserHistory

使用hashHistory,浏览器的url是这样的：/#/user/liuna?_k=adseis  
使用browserHistory,浏览器的url是这样的：/user/liuna

[router的使用](https://www.cnblogs.com/liuna/p/6137970.html)  
[在React中使用react-router-dom路由](https://www.jianshu.com/p/8954e9fb0c7e)   

### 使用 withRouter
引入withRouterimport { withRouter } from "react-router-dom"

然后用高阶组件withRouter把要导出的组件传入进去
最后使用this.props.history.push()把你需要跳转的路由push进去就好了


[react-router v4 手动控制路由跳转](https://www.jianshu.com/p/52528ebb771d)