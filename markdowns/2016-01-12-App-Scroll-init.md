---
title:  移动端滚动与内置浏览器出界问题
date: 2016-01-12
tags: App
---

### 快速回弹滚动以及微信架构页面的思考

我们先来看看回弹滚动在手机浏览器发展的历史：
早期的时候，移动端的浏览器都不支持非body元素的滚动条，所以一般都借助 iScroll;
Android 3.0/iOS解决了非body元素的滚动问题，但滚动条不可见，同时iOS上只能通过2个手指进行滚动；
Android 4.0解决了滚动条不可见及增加了快速回弹滚动效果，不过随后这个特性又被移除；
iOS从5.0开始解决了滚动条不可见及增加了快速回弹滚动效果

<!--more-->

#### 滚动说明

全局滚动， 滚动条在body节点或更顶层
局部滚动， 滚动条在body下某一个dom节点上

### ios

```
body{
	-webkit-overflow-scrolling: touch;
}
```
这个属性最好绑定在父级，或者更上一级，绑定在body上有时候失灵。父级给个固定高度会更好

这个属性可以实现类似原生的效果，快速回弹。
但是会出项出界问题，就是当你在微信或者QQ中打开页面的时候，滚动的时候，你会看看‘网页通过‘’提供支持’一个黑色的背景样式。

##### 考虑换一个思想，局部滚动

+ body加上-webkit-overflow-scrolling: touch;
+ 通过 [ScrollFix](https://github.com/joelambert/ScrollFix) 解决出界问题

### Android

-webkit-overflow-scrolling: touch 在Android在没有效果，而且用类似ios那个方法比较的坑爹，滚动条不能实时滚动

#### 用全局滚动效果

+ header, footer 用fixed属性固定
+ 内容区域用padding 填充上下的高度问题

## 最终实现方案

+ 第一步先通过 UA判断 客户端类型 [检测客户端](https://github.com/dukegod/isClient)
+ 分不同的客户端加载不同的样式
+ 对于需要固定部分，取消默认的touchmove 属性

[项目地址](https://github.com/dukegod/h5-demos/tree/master/demos/fastScroll)
