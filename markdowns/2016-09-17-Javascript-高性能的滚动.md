---
title:  scroll
date: 2016-09-17
tags: [JavaScript]
---

前面的文章分析节流与去抖的概念，用法，区别。这次总结，在实际项目中的应用

### 使用 rAF（requestAnimationFrame）触发滚动事件

上面介绍的抖动与节流实现的方式都是借助了定时器 setTimeout ，但是如果页面只需要兼容高版本浏览器或应用在移动端，又或者页面需要追求高精度的效果，那么可以使用浏览器的原生方法 rAF（requestAnimationFrame）。

requestAnimationFrame

window.requestAnimationFrame()这个方法是用来在页面重绘之前，通知浏览器调用一个指定的函数。这个方法接受一个函数为参，该函数会在重绘前调用。

rAF 常用于 web 动画的制作，用于准确控制页面的帧刷新渲染，让动画效果更加流畅，当然它的作用不仅仅局限于动画制作，我们可以利用它的特性将它视为一个定时器。（当然它不是定时器）

通常来说，rAF 被调用的频率是每秒 60 次，也就是 1000/60 ，触发频率大概是 16.7ms 。（当执行复杂操作时，当它发现无法维持 60fps 的频率时，它会把频率降低到 30fps 来保持帧数的稳定。）

```
var ticking = false; // rAF 触发锁

function onScroll(){
  if(!ticking) {
    requestAnimationFrame(realFunc);
    ticking = true;
  }
}

function realFunc(){
    // do something...
    console.log("Success");
    ticking = false;
}
// 滚动事件监听
window.addEventListener('scroll', onScroll, false);
```

使用 requestAnimationFrame 优缺点并存，首先我们不得不考虑它的兼容问题，其次因为它只能实现以 16.7ms 的频率来触发，代表它的可调节性十分差,16.7ms 触发一次 handler，降低了可控性，但是提升了性能和精确度。


https://github.com/hanzichi/underscore-analysis/issues/20

https://www.shiyanlou.com/questions/4303
