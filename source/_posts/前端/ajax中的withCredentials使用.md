---
title:  ajax中的withCredentials使用
tags:  [跨域请求是否提供凭据信息cookie]
categories: [前端]
---

#### XMLHttpRequest.withCredentials 有什么用?
跨域请求是否提供凭据信息(cookie、HTTP认证及客户端SSL证明等)
也可以简单的理解为，当前请求为跨域类型时是否在请求中协带cookie。
XMLHttpRequest.withCredentials 怎么用?
withCredentials属于XMLHttpRequest对象下的属性，可以对其进行查看或配置。

```
var xhr = new XMLHttpRequest();
xhr.open('GET', 'http://172.19.0.215:1314/learnLinkManager/getLearnLinkList', true); 
xhr.withCredentials = true; //关键设置
xhr.onreadystatechange = function() {
  console.log('withCredentials=>', xhr.withCredentials);
};
xhr.send(null);

```

[ajax中的withCredentials使用效果](https://www.jianshu.com/p/af1fc0fab4c5)  
[跨域请求设置withCredentials](https://www.cnblogs.com/zhangcybb/p/6594991.html)  
[跨域请求带cookie的解决方案](https://blog.csdn.net/sysuzjz/article/details/51566713)