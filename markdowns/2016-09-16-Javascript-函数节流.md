---
title:  函数节流
date: 2016-09-16
tags: [JavaScript]
---

简单的说：函数节流能使得连续的函数执行，变为 固定时间段 间断地执行。

节流函数：只允许一个函数在X毫秒内执行一次，只有当上一次函数执行后过了你规定的时间间隔，才能进行下一次该函数的调用。

throttle 和 debounce 的应用场景

+ 按一个按钮发送 AJAX：
给 click 加了 debounce 后就算用户不停地点这个按钮，也只会最终发送一次；如果是 throttle 就会间隔发送几次

+ 监听滚动事件判断是否到页面底部自动加载更多：
给 scroll 加了 debounce 后，只有用户停止滚动后，才会判断是否到了页面底部；如果是 throttle 的话，只要页面滚动就会间隔一段时间判断一次


[详情参考此项目案例](https://github.com/dukegod/h5-demos/tree/master/demos/throttle)


## 参考

https://github.com/hanzichi/underscore-analysis/issues/22

https://keelii.github.io/2016/06/11/javascript-throttle/
