---
title: 移动开发点击事件
date: 2016-01-07
tags: App
---
#### 移动页面300ms延迟

#### 产生的原因

2007年苹果发布首款iphone上IOS系统搭载的safari为了将适用于PC端上大屏幕的网页能比较好的展示在手机端上，使用了双击缩放(double tap to zoom)的方案，比如你在手机上用浏览器打开一个PC上的网页，你可能在看到页面内容虽然可以撑满整个屏幕，但是字体、图片都很小看不清，此时可以快速双击屏幕上的某一部分，你就能看清该部分放大后的内容，再次双击后能回到原始状态。
双击缩放是指用手指在屏幕上快速点击两次，iOS 自带的 Safari 浏览器会将网页缩放至原始比例。
原因就出在浏览器需要如何判断快速点击上，当用户在屏幕上单击某一个元素时候，例如跳转链接，此处浏览器会先捕获该次单击，但浏览器不能决定用户是单纯要点击链接还是要双击该部分区域进行缩放操作，所以，捕获第一次单击后，浏览器会先Hold一段时间t，如果在t时间区间里用户未进行下一次点击，则浏览器会做单击跳转链接的处理，如果t时间里用户进行了第二次单击操作，则浏览器会禁止跳转，转而进行对该部分区域页面的缩放操作。那么这个时间区间t有多少呢？在IOS safari下，大概为300毫秒。这就是延迟的由来。造成的后果用户纯粹单击页面，页面需要过一段时间才响应，给用户慢体验感觉，对于web开发者来说是，页面js捕获click事件的回调函数处理，需要300ms后才生效，也就间接导致影响其他业务逻辑的处理。

<!--more-->

#### 解决方案：

+ fastclick可以解决在手机上点击事件的300ms延迟
+ zepto的touch模块，tap事件也是为了解决在click的延迟问题

#### 触摸事件的响应顺序

1. ontouchstart
2. ontouchmove
3. ontouchend
4. onclick

解决300ms延迟的问题，也可以通过绑定ontouchstart事件，加快对事件的响应。

#### 屏蔽ios和android下点击元素时出现的 **阴影块**

```
a{
	-webkit-tap-highlight-color:rgba(255,255,255,0);
	font-size: 20px;
}
```

先去除阴影块的影响（不过有的产品需要这个效果），接下来继续说说给移动端添加点击效果。

#### hover 属性 **阴影点**

可以最开始想的都是这个，当时在实际项目中，我们发现，当我们点击的时候，确实可以出现效果，但是这个效果就一直存在，除非我们刷新页面。还有就是只要自己的手放上去就会有触发，体验不好。

#### active 属性


```
a{
-webkit-tap-highlight-color:rgba(255,255,255,0);
font-size: 20px;
display: block;
margin-top: 10px;
}
a:hover{
	color: black;
}
a:active{
	color: red;
	font-size: 24px;
}
```

实际上效果，在iPhone上没有active效果，但是在红米上有效果，UC浏览器也没有active效果。手机兼容性不是很好。

#### 原生js实现

通过一系列的探索，又回到了js上。

##### 国外有个激活css的active效果

```
document.addEventListener("touchstart", function(){}, true)
```

这次iPhone没有问题了，但是在Android手上有问题了，红米上反应迟钝，UC没有效果


#### 绑定ontouchstart和ontouchend来控制按钮的类名

```
var btn = document.querySelector('.btn-blue');
btn.addEventListener("touchstart", function(){
	console.log('stat');
	this.className = 'btn-blue btn-blue-on'
}, false)
btn.addEventListener("touchend", function(){
	console.log('end');
	this.className = 'btn-blue'
}, false)
```

#### 封装一个用jquery插件

可以修改相应事件，背景色

**[项目地址](https://github.com/dukegod/jqueryTapTrace)**

### 参考

http://jsfiddle.net/prud/x9y6cfhg/
