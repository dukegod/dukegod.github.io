---
title:  reduce
date: 2016-09-08
tags: JavaScript
---

指定的函数将数组元素进行组合,生成单个值.

```
[].reduce(function(previousValue, currentValue, index, array){
  return previousValue + currentValue;
},initValue);

```
<!-- more -->

回调函数第一次执行时，previousValue 和 currentValue 可以是一个值，如果 initialValue 在调用 reduce 时被提供，那么第一个 previousValue 等于 initialValue ，并且currentValue 等于数组中的第一个值；如果initialValue 未被提供，那么previousValue 等于数组中的第一个值，currentValue等于数组中的第二个值

未给赋初始值

```
var arr = [1,2,3,4,5];
var sum = arr.reduce(function(a,b){
  console.log('a----',a);
  console.log('b',b);
  return a+b
});
console.log(sum)

/**
 * 返回的结果作为第一个参数的回调
 *
 */

```
给赋初始值

```
var arr = ['a', 'b', 'c', 'd', 'a', 'a', 'b', 'c'];
var ii =arr.reduce(function (p, k, index, array) {
  return p[k] ? (p[k]++) : (p[k] = 1), p;
},{});

console.log(ii)

/**
 * reduce 接受一个对象{}最为初始值，每次执行的结果作为p的回调结果继续执行，一直到最后一个k结束
 *
 * return 顺序执行，先判断对象有没有这个属性，没有就赋值为1，有了就加1，最后返回p继续回调
 */

```