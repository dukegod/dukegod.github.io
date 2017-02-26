---
title: Node 模块化
date: 2016-10-29
tags: [Node]
---

### exports 模块调用

```
// a.js
function A(){}
exports.A = A;
// 引用
let AA = require('./a');
console.log(AA); // { A: [Function: A }
AA.A();
```
exports返回的是一个对象，引用的时候需要调用这个函数名称.

### module 模块调用

创建全局对象  
通过module调用函数直接返回全局对象，返回的函数直接可以调用

```
//em.js
function em(){
  console.log('module function');
}

module.exports = em;
// 调用
let callem = require('./em');
console.log(callem) // [Function: em]
callem()
```
自动执行函数

```
// 自动执行写法
module.exports = function(){}()

<!-- es6 写法 -->
module.exports = ()=>{}
// 自动执行函数  
module.exports = (()=>{})()
```
返回多个函数，返回值以对象的方式返回

```
const name = 'duke';
function showName(name){
  console.log(name);
}
module.exports = {name, showName}
// 返回值类型
{ name: 'duke', showName: [Function: showName] }
```

### 配合es2015 class写法

```
class Point{}
module.exports = Point  
```

**注意与es2015原生js写法的不同**
