---
title:  ajax note
date: 2016-01-22
tags: [JavaScript,Ajax,Http]
---

ajax的全称是Asynchronous JavaScript and XML

### 原理与主要的技术点

Ajax的原理简单来说通过XmlHttpRequest对象来向服务器发异步请求，从服务器获得数据，然后用javascript来操作DOM而更新页面。

<!--more-->

#### XMLHttpRequest对象

##### 主要方法：

+ open("method","URL",[asyncFlag],["userName"],["password"]):

建立对服务器的调用。method参数可以是GET、POST或PUT。url参数可以是相对URL或绝对URL。这个方法还包括3个可选的参数，是否异步，用户名，密码;

+ send(content)

向服务器发送请求

+ setRequestHeader

把指定首部设置为所提供的值。在设置任何首部之前必须先调用open()。设置header并和请求一起发送 ('post'方法一定要 )

##### 主要属性

+ onreadystatechange

状态改变的事件触发器，每个状态改变时都会触发这个事件处理器，通常会调用一个JavaScript函数

+ readyState

请求的状态。有5个可取值：0 = 未初始化，1 = 正在加载，2 = 已加载，3 = 交互中，4 = 完成

+ responseText

服务器的响应，返回数据的文本。

+ responseXML

服务器的响应，返回数据的兼容DOM的XML文档对象 ，这个对象可以解析为一个DOM对象。

+ responseBody

服务器返回的主题（非文本格式）

+ responseStream

服务器返回的数据流

+ status

服务器的HTTP状态码（如：404 = "文件末找到" 、200 ="成功" ，等等）

+ statusText

服务器返回的状态文本信息 ，HTTP状态码的相应文本（OK或Not Found（未找到）等等）

#### 简单的封装（不考虑IE）

get方法

```
function ajaxGet(){
	var request = new XMLHttpRequest();
	request.open("GET", "server.php?number=" + document.getElementById("keyword").value);
	request.send();
	request.onreadystatechange = function() {
		if (request.readyState===4) {
			if (request.status===200) {
				document.getElementById("searchResult").innerHTML = request.responseText;
			} else {
				alert("发生错误：" + request.status);
			}
		}
	}
}
```

post方法

```
function ajaxPOST() {
	var request = new XMLHttpRequest();
	request.open("POST", "server.php");
	var data = "name=" + document.getElementById("staffName").value
	                  + "&number=" + document.getElementById("staffNumber").value
	                  + "&sex=" + document.getElementById("staffSex").value
	                  + "&job=" + document.getElementById("staffJob").value;
	request.setRequestHeader("Content-type","application/x-www-form-urlencoded");
	request.send(data);
	request.onreadystatechange = function() {
		if (request.readyState===4) {
			if (request.status===200) {
				document.getElementById("createResult").innerHTML = request.responseText;
			} else {
				alert("发生错误：" + request.status);
			}
		}
	}
}
```

#### 使用封装好的库

##### jquery

$.ajax()

zepto 类似

### 跨域

一个域名组成：http：//www.22.com:8080/js.js:  协议，子域名，主域名，端口号，请求资源地址

同源是指，域名，协议，端口相同

当协议，子域名，主域名端口号中任意一个不相同时，都算作不同域

不同域名之间相互请求资源都算作“跨域”

### 解决方法

1. 浏览器的同源策略把跨域请求都禁止了但是HTML的script标签是例外，可以突破同源策略从其他来源获取数据；我们可以通过script标签引入jsonp文件，然后通过一系列JS操作获取数据。

原生js

```
function jsonHandle(url) {
    var script = document.createElement("script");
    script.setAttribute("src",url);
    document.getElementsByTagName("body")[0].appendChild(script);
}
//JS插入之后就可以处理数据了
```

jquery 封装jsonp方法

```
$.ajax({
   type: "GET",
	url: "http://127.0.0.1/ajax/serverjsonp.php",
	dataType: "jsonp",
	jsonp: "callback", // 前后端协调命名的
	success: function(data) {
		if (data.success) {
			$("#searchResult").html(data.msg);
		} else {
			$("#searchResult").html("出现错误：" + data.msg);
		}
	},
	error: function(jqXHR){
	   alert("发生错误：" + jqXHR.status);
	},
});
```

但是jsonp 只能解决get方法的跨域请求

2. HTML5提供的XML HttpRequest level2（IE10 一下不支持）

修改服务端

```
header('Access-Control-Allow-Origin:*');
header('Access-Control-Allow-Methods:POST,GET');
header('Access-Control-Allow-Credentials:true');
header("Content-Type: application/json;charset=utf-8");
```
详情见 XMLHttpRequestXHR2.html

[项目地址](https://github.com/dukegod/phpBasic/tree/master/ajax)

## 参考

[AJAX工作原理及其优缺点](http://www.cnblogs.com/sanmaospace/archive/2013/06/15/3137180.html)

[jsonp](https://segmentfault.com/a/1190000002799156)



