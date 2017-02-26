---
title: 项目开发规范之编写可维护的JavaScript笔记
date: 2016-06-20
tags: [开发规范]
---

本文依据《编写可维护的JavaScript》，然后平时开发中遇到的问题，综合总结如下：

## 缩进层级

space, 2个字符

<!-- more -->

## 命名

### 变量

驼峰命名法

```
var data;

var dateList;

function renderDate(){}

var renderDate = function(){}

```

### 常量

大写字母和下划线

```
var COUNT = 10;

var MAX_COUNT = 100;

```

### 函数

驼峰命名法

```
function renderDate(){}

var renderDate = function(){}

```

### 构造函数

驼峰命名法，首字母大写

```
function Person(){}

Person.prototype.show = function(){}

Person.prototype.showName = function(){}

```

### 直接量

字符串，数字，布尔值，null，undefined

```

var string = 'abdddd' ;

var number = 90;

var person = null;

if (preson !== null){
  console.log('yes');
}

```

### 对象直接量

使用对象直接量创建对象

```
var obj = {
  name : 'lh',
  workplace ; 'jd'
}
```

### 数组直接量

```
var arr = [];

var array = [1, 2, 3];
```

## 注解

### 单行注解

```
// no use
```

### 多行注解

```
/*
*
*/
```

## 语句与表达式

### 花括号对齐

```
function (){

}
```

### 块状句间隔

在括号后面加上空格

```
if() {

}
```

## 变量，函数，运算符

### 变量声明

最好先声明后再用

```
function doSometing(){}

doSomething();
```

### 立即调用函数

最好用一个圆括号包裹起来

```
var value = (function() {
  // 函数体

  return {
    message : 'hi'
  }
}());

```

### 相等

JavaScript中存在强类型转换然后去判断。

推荐使用 === 与 !==

```
// 5 '5'
console.log(5 == '5'); // true
console.log(5 === '5'); // false

// 25 与 十六进制25
console.log(25 == 'ox19'); // true
console.log(25 === 'ox19'); // false

// 数字0 与 false
console.log(0 == false); // true
console.log(0 === false); // false

// 数字1 与 true
console.log(1 == true); // true
console.log(1 === true); // false

// 数字2 与 false
console.log(2 == true); // false
console.log(2 === true); // false


// null 与 undefined
console.log(null == undefined); // true
console.log(null === undefined); // false

var object = {
  toString: function() {
    return 'ox19'
  }
}
// object 与 25
console.log(object == 25) // true
console.log(object === 25) // false

```

## 避免全局变量

特别是var的使用

### 单全局变量

既是所创建的这个唯一的全局对象名是独一无二的，并将你所有的功能代码都挂载到这个全局对象上。

如jquery定义了两个全局对象，$与jQuery。

```
function Person(name) {
  this.name = name;
}
Person.prototype.show = function() {}

var p1 = new Person('a1');
var p2 = new Person('a2');
var p3 = new Person('a3');

```

上面的代码出现了4个全局变量。 Person, p1, p2, p3。使用单全局变量原则后：

```
var onlyFunc = {}

onlyFun.Person = function(name) {
  this.name = name;
}

onlyFun.Person.prototype.show = function() {}

onlyFun.p1 = new onlyFun.Person('a1');
onlyFun.p2 = new onlyFun.Person('a2');
onlyFun.p3 = new onlyFun.Person('a3');

```

### 零全局变量

使用函数包装器

(function(win) {
  // body
  var doc = document;

}(window))

## 事件处理

抽离出事件参数，越精细越好。

## 避免空比较

### 使用typeof检测原始对象

检测的对象： string，number，boolean，undefined

使用===，与！==检测

null不作为检测对象，如果需要检测使用===，与！==检测

### 检测引用值，instanceof

typeof用来检测基本类型可以，检测引用值有点力不从心。好多类型都会报出为object。

使用instanceof：

```
// yongfa
value instanceof constructor

value instanceof Date

value instanceof RegExp

value instanceof Error

function Person(name) {
  this.name = name;
}
var me = new Person('lh');

me instanceof Person

```

### 检测函数

检测函数最好的方法就是使用typeof，可以跨帧（frame）使用

### 检测数组

由于存在桢数组来回传递，最终检测方案

```

function isArray(value) {
  if(typeof Array.isArray === 'function') {
    return Array.isArray(value);
  } else {
    return Object.prototype.toString.call(value) === 'object Array'
  }
}

```

### 检测属性

使用in或者hasOwnProperty()

```
var obj = {
  title: 'lh'
}

if('title' in obj) {
}

if(obj.hasOwnProperty('title')) {

}

```

## 将配置数据从代码中分离出来

```
var CONFIG = {
  MSG_NAME: 'LH',
  MSGE_AGE; '19'
}

```

## 抛出错误类型

try-catch-finally

throw














