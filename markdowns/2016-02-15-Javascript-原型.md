---
title: 原型
date: 2016-02-15
tags: [JavaScript]
---

1. 构造函数.prototype = 原型对象

2. 原型对象.constructor = 构造函数(模板)

3. 原型对象.isPrototypeof(实例对象)   判断实例对象的原型 是不是当前对象

4. 单全局变量,使用一个最外层的对象进行包裹，所有的功能都挂载在是上面（详情见-2016-06-21）


每一个对象创建的时候都会有一个prototype属性。

```js
var Person = function(){};

console.log(typeof Person); // function
console.log(Person.prototype); // {}
console.log(Person.prototype.constructor); //[Function]

```

空函数，prototype指向本身，constructor指向最高一级［Function］。原型链查找就是层级向上查找的。

```js
var Person = function(name){
	this.name = name;
};
Person.prototype.common = function(){
	console.log('person common prototype');
}
var person = new Person('duke');
var person2 = new Person('duke2');

console.log(Person.prototype); //  common: [Function] }
console.log(Person.prototype.constructor == Person); // ture
console.log(person.constructor);[Function]
console.log(person.constructor == Person);// ture
console.log(typeof person); // object
console.log(person.prototype); // undefined
console.log(person.prototype.constructor); // error

```

实例方法的constructor指向构造方法，构造函数的属性的constructor指向构造函数本身。

最好的实现，应用 寄生组合式模式开发。

```
var Person = function(){};
Person.prototype.showName = function(){};
var p = new Person();
console.log(p instanceof Person);
console.log(Person.prototype);
console.log(Person.constructor === Function); // 构造函数的constructor指向Function
console.log(p.constructor === Person); // 实例函数的constructor指向构造函数
console.log(p.prototype);

console.log('Child');
var Child = function(){};
Child.prototype = Person.prototype;
Child.prototype.constructor = Child; // 没有这条，ch.constructor ！== Child 而是指向ch.constructor === Person
var ch = new Child();
console.log(ch instanceof Child);
console.log(Child.prototype);
console.log(Child.constructor === Function);
console.log(ch.constructor === Person);
console.log(ch.constructor === Child);
console.log(ch.prototype);

```

使用原型链实现继承的时候，我们需要注意的点。

因为Child.prototype = Person.prototype，所以我们需要手动的把Child.prototype.constructor重新修改为指向自己，否则实例对象的constructor都是指向Person。

[原型，类，构造方法](https://keelii.github.io/2016/07/02/javascript-definitive-guide-note-8/)
