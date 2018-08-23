---
title:  web页面打开APP
tags:  [web页面打开APP]
categories:  [前端]
date:  2018-06-11 16:17:22
---

### 在WXApp上设置一个URL Schemes

```
为了能让别的App(包括我们刚才创建的MyApp)能够打开 OpenTest，
我们需要为app添加一个URL Schemes。
步骤：选中app工程->Info->URL Types->点击“+”->在URL Schemes栏填上 OpenTest
```

### 打开APP  xxx.html

>可以保存一下页面为.html 放在本地服务Document目录下 快速启动

```html
<html>
	<head>
	    <meta charset="UTF-8">
	    <meta content="text/html; charset=utf-8" http-equiv="Content-Type">
	    <meta name="HandheldFriendly" content="true"/>
	    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">

		<script type="text/javascript">

		function open_win() 
		{
		window.open("OpenTest")
		// window.open("http://www.baidu.com")
		}
		</script>
	</head>
	
	<body>
		<div style="width:100%;height: 100%;background: white; position: absolute;">
			<!-- 方法一 -->
			<a style="margin-top:200px; width:100%;color:#666; font-size:32px; text-align: center ;display:inline-block;"
			href="OpenTest" target="_blank">打开OpenTest App页面</a>
		</div>

		<!-- OpenTest -->

		<!-- 方法二跳转有点问题 -->
		<!-- <input type=button 
		style="width:250px; height=200px;"
		size="60"
		value="dsl open 打开" onclick="open_win()" /> -->

	</body>
</html>
```
 