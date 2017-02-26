---
title: 前端开发模块管理
date: 2016-05-25
tags: [JavaScript, 开发工具]
---
伴随着移动互联的大潮，当今越来越多的网站已经从网页模式进化到了 Webapp 模式。它们运行在现代的高级浏览器里，使用 HTML5、 CSS3、 ES6 等更新的技术来开发丰富的功能，网页已经不仅仅是完成浏览的基本需求，并且webapp通常是一个单页面应用，每一个视图通过异步的方式加载，这导致页面初始化和使用过程中会加载越来越多的 JavaScript 代码，这给前端开发的流程和资源组织带来了巨大的挑战。

前端开发和其他开发工作的主要区别，首先是前端是基于多语言、多层次的编码和组织工作，其次前端产品的交付是基于浏览器，这些资源是通过增量加载的方式运行到浏览器端，如何在开发环境组织好这些碎片化的代码和资源，并且保证他们在浏览器端快速、优雅的加载和更新，就需要一个模块化系统，这个理想中的模块化系统是前端工程师多年来一直探索的难题。

<!-- more -->

## 模块系统演化

模块系统主要解决模块的定义、依赖和导出，先来看看已经存在的模块系统。

### <script>标签

```js
<script src="module1.js"></script>
<script src="module2.js"></script>
<script src="libraryA.js"></script>
<script src="module3.js"></script>
```

这是最原始的 JavaScript 文件加载方式，如果把每一个文件看做是一个模块，那么他们的接口通常是暴露在全局作用域下，也就是定义在 `window` 对象中，不同模块的接口调用都是一个作用域中，一些复杂的框架，会使用命名空间的概念来组织这些模块的接口，典型的例子如 [YUI](http://yuilibrary.com) 库。

这种原始的加载方式暴露了一些显而易见的弊端：

-  全局作用域下容易造成变量冲突
-  文件只能按照 `<script>` 的书写顺序进行加载
-  开发人员必须主观解决模块和代码库的依赖关系
-  在大型项目中各种资源难以管理，长期积累的问题导致代码库混乱不堪

### CommonJS

服务器端的 Node.js 遵循 [CommonJS规范](http://wiki.commonjs.org/wiki/CommonJS)，该规范的核心思想是允许模块通过 `require` 方法来同步加载所要依赖的其他模块，然后通过 `exports` 或 `module.exports` 来导出需要暴露的接口。

```js
require("module");
require("../file.js");
exports.doStuff = function() {};
module.exports = someValue;
```

优点：

-  服务器端模块便于重用
-  [NPM](https://www.npmjs.com) 中已经有将近20万个可以使用模块包
-  简单并容易使用

缺点：

-  同步的模块加载方式不适合在浏览器环境中，同步意味着阻塞加载，浏览器资源是异步加载的
-  不能非阻塞的并行加载多个模块

实现：

-  服务器端的 [Node.js](http://www.nodejs.org)
-  [Browserify](http://browserify.org)，浏览器端的 CommonJS 实现，可以使用 NPM 的模块，但是编译打包后的文件体积可能很大
-  [modules-webmake](https://github.com/medikoo/modules-webmake)，类似Browserify，还不如 Browserify 灵活
-  [wreq](https://github.com/substack/wreq)，Browserify 的前身

### AMD

[Asynchronous Module Definition](https://github.com/amdjs/amdjs-api) 规范其实只有一个主要接口 `define(id?, dependencies?, factory)`，它要在声明模块的时候指定所有的依赖 `dependencies`，并且还要当做形参传到 `factory` 中，对于依赖的模块提前执行，依赖前置。

AMD（异步模块定义）是为浏览器环境设计的，因为 CommonJS 模块系统是同步加载的，当前浏览器环境还没有准备好同步加载模块的条件。

优点：

-  适合在浏览器环境中异步加载模块
-  可以并行加载多个模块

缺点：

-  提高了开发成本，代码的阅读和书写比较困难，模块定义方式的语义不顺畅
-  不符合通用的模块化思维方式，是一种妥协的实现

实现：

-  [RequireJS](http://requirejs.org)
-  [curl](https://github.com/cujojs/curl)

#### requirejs 简单介绍

在 Require.js 中模块名是全局作用域，可以在全局引用

```
define(id?: String, dependencies?: String[], factory: Function|Object);

define(function(require, exports, module) {}）

```

id 是模块的名字，它是可选的参数。

dependencies 指定了所要依赖的模块列表，它是一个数组，也是可选的参数，每个依赖的模块的输出将作为参数一次传入 factory 中。如果没有指定 dependencies，那么它的默认值是 ["require", "exports", "module"]

factory 是最后一个参数，它包裹了模块的具体实现，它是一个函数或者对象。如果是函数，那么它的返回值就是模块的输出接口或值。


### CMD

[Common Module Definition](https://github.com/cmdjs/specification/blob/master/draft/module.md) 规范和 AMD 很相似，尽量保持简单，并与 CommonJS 和 Node.js 的 Modules 规范保持了很大的兼容性。

```js
define(function(require, exports, module) {
  var $ = require('jquery');
  var Spinning = require('./spinning');
  exports.doSomething = ...
  module.exports = ...
})
```

优点：

-  依赖就近，延迟执行
-  可以很容易在 Node.js 中运行

缺点：

-  依赖 SPM 打包，模块的加载逻辑偏重

实现：

-  [Sea.js](http://seajs.org/)
-  [coolie](https://github.com/cloudcome/coolie)

### UMD

[Universal Module Definition](https://github.com/umdjs/umd) 规范类似于兼容 CommonJS 和 AMD 的语法糖，是模块定义的跨平台解决方案。

使用一下方式，兼容各个模式与浏览器方式引用

```
(function (global, factory) {
  if (typeof define === 'function' && define.amd) {
    // AMD环境中
    define( function () {
      return factory(global);
    });
  } else if (typeof module !== 'undefined' && module.exports) {
    // CMD环境中
    module.exports = factory(global);
  } else {
    // 浏览器环境，添加到global中
    global.getDateInstance = factory(global);
  }
}(typeof window !== 'undefined' ? window : this, function(window) {
  // 抛出去函数方法
  var getDateInstance = {};
}))


```

### ES6 模块

EcmaScript6 标准增加了 JavaScript 语言层面的模块体系定义。[ES6 模块](http://es6.ruanyifeng.com/#docs/module)的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。

```js
import "jquery";
export function doStuff() {}
module "localModule" {}
```

优点：

-  容易进行静态分析
-  面向未来的 EcmaScript 标准

缺点：

-  原生浏览器端还没有实现该标准
-  全新的命令字，新版的 Node.js才支持

实现：

-  [Babel](https://babeljs.io/)

### 期望的模块系统

可以兼容多种模块风格，尽量可以利用已有的代码，不仅仅只是 JavaScript 模块化，还有 CSS、图片、字体等资源也需要模块化。

见 webpack 总结

### 参考

[webapack](http://webpackdoc.com/index.html)
