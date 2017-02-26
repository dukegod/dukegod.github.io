---
title: 移动端对touchmove支持度不同
date: 2017-01-18
tags: [JavaScript,Hack]
---
有的手机支持touchmove方法不是很理想。开发中遇到的如oppo,Nubia

把对touchmove的监听，换做对scroll的监听

```
document.getElementById('category-content-list').addEventListener('touchmove',function(){
},false)

// 换做如下
document.getElementById('category-content-list').addEventListener('scroll',function(){
},false)

```
