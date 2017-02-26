---
title: Bind
date: 2016-02-16
tags: [JavaScript]
---

bind()方法会创建一个新函数，当这个新函数被调用时，它的this值是传递给bind()的第一个参数, 它的参数是bind()的其他参数和其原本的参数

```
fn.bind(a,b,c,d);
```

+ this值绑定到第一个参数(a),[null，undefined表示调用自身]
+ 其他的参数添加到a以后
+ bind 返回的是一个没有执行的函数

```
var obj = {
  a: 1,
  b: 2,
  getCount: function(c, d) {
    return this.a + this.b + c + d;
  }
};

Function.prototype.bind = Function.prototype.bind || function(context) {
  var that = this;
  return function() {
    // console.log(arguments); // console [3,4] if ie<6-8>
    return that.apply(context, arguments);

  }
}
window.a = window.b = 0;
var func = obj.getCount.bind(obj);
console.log(func(3, 4));  // 10

// 用apply调用
var ans = obj.getCount.apply(obj, [3, 4]);
console.log(ans); // 10
```
以上说明第三点，bind返回一个未执行的函数


bind()提供this的上下文

```
var slice = Function.prototype.call.bind(Array.prototype.slice);

console.log(slice)// function call(){}

slice([1,2,3],0,1);
```
理解为，我们先绑定了slice，这个时候this已经指向slice这个方法，    
然后我们再去通过call在绑定一次，把以前绑定的方法作为call的方法，去执行。


待研究：
+ [函数借用](http://www.zcfy.cc/article/borrowing-methods-in-javascript-by-david-shariff-794.html)
+ [函数柯里化](http://liuwanlin.info/javascriptzhong-bindfang-fa-de-shi-xian/)


[mozilla](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
[参考](http://www.cnblogs.com/zichi/p/4357023.html)
[hanzichi](https://github.com/hanzichi/underscore-analysis/issues/18)
