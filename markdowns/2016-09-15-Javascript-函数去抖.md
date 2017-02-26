---
title:  函数去抖
date: 2016-09-15
tags: [JavaScript]
---
函数去抖的核心既是**对于一定时间段的连续的函数调用，只让其执行一次就好了**。节约浏览器的性能。

防抖动：防抖技术即是可以把多个顺序地调用合并成一次，也就是在一定时间内，规定事件被触发的次数。

应用场景：
+ 浏览器resize，scroll
+ ajax的输出验证，一定时间只让其做一次验证

<!-- more -->

```
var _debounce = function(func, wait, immediate) {
  var timeout, args, context, timestamp, result;
  var later = function() {
    // 据上一次触发时间间隔
    var last = Date.now() - timestamp;
    // 上次被包装函数被调用时间间隔last小于设定时间间隔wait
    if (last < wait && last > 0) {
      timeout = setTimeout(later, wait - last);
    } else {
      timeout = null;
      // 如果设定为immediate===true，因为开始边界已经调用过了此处无需调用
      if (!immediate) {
        result = func.apply(context, args);
        if (!timeout) context = args = null;
      }
    }
  };
  return function() {
    context = this;
    args = arguments;
    timestamp = Date.now();
    var callNow = immediate && !timeout;
    // 如果延时不存在，重新设定延时
    if (!timeout) timeout = setTimeout(later, wait);
    if (callNow) {
      result = func.apply(context, args);
      context = args = null;
    }
    return result;
  };
};
```
实现一个滚动加载的优化方案

```
document.getElementById('container').addEventListener('scroll', _debounce(isScroll, 100), false);

```

可以通过lodash-cli 生成自己需要的文件

[详情参考此项目案例](https://github.com/dukegod/h5-demos/tree/master/demos/debounce)


## 参考

https://github.com/hanzichi/underscore-analysis/issues/21
