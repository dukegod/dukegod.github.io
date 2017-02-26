---
title: Browserify
date: 2016-05-31
tags: [开发工具]
---

Browserify 可以让你使用类似于 node 的 require() 的方式来组织浏览器端的 Javascript 代码，通过预编译让前端 Javascript 可以直接使用 Node NPM 安装的一些库

Browserify解决了js在浏览器端的依赖问题

browserify是一个编译工具,通过它可以在浏览器环境下像nodejs一样使用遵循commonjs规范的模块化编程.

你可以使用browserify来组织代码,也可以使用第三方模块,不需要会nodejs,只需要用到node来编译,用到npm来安装包.

browserify模块化的用法和node是一样的,所以npm上那些原本仅仅用于node环境的包,在浏览器环境里也一样能用.

现在npm上有越来越多的包,在设计的时候就是想好既能在node环境下用,也能在浏览器环境下用的.甚至还有很多包就是给浏览器环境使用的. npm是为所有的javascript服务的,无论前端后端.

<!-- more -->

## gulp + browserify

```
var gulp = require("gulp");
var browserify = require("browserify");
var sourcemaps = require("gulp-sourcemaps");

//用于将Browserify的bundle()的输出转换为Gulp可用的[vinyl][]（一种虚拟文件格式）流
var source = require('vinyl-source-stream');

//用于将vinyl流转化为buffered vinyl文件（gulp-sourcemaps及大部分Gulp插件都需要这种格式）
var buffer = require('vinyl-buffer');

gulp.task("browserify", function () {
  var b = browserify({
      entries: "./javascripts/src/main.js",
      debug: true
  });

  return b.bundle()
    .pipe(source("bundle.js"))
    .pipe(buffer())
    .pipe(sourcemaps.init({loadMaps: true}))
    .pipe(sourcemaps.write("."))
    .pipe(gulp.dest("./javascripts/dist"));
});

```
#### watchify

browserify和watchify是同一个作者的作品，browserify的作用是把分析js源文件的依赖关系，把N个js文件”编译”成一个js文件；而browserify在编译时，没有缓存，即当文件修改时，所有的文件都要重新编译一遍，这样编译时间就比较长（其实也不算长，基本上几秒钟搞定）；watchify为browserify加上缓存功能，当文件发生变化时，只编译修改过的文件，这样就大幅缩短了编译时间，重新编译基本上不到1秒。

#### 输出多个bundle文件

文件中通过require(或者import) 方式加载依赖文件

通过循环的方式按照文件目录输出

#### 处理zepto

zepto-browserify插件


[gulp+browserify+watchify用例](https://github.com/vigetlabs/gulp-starter)

## 问题总结

```
SyntaxError: 'import' and 'export' may appear only with 'sourceType: module'
```

解决方案见:[stackoverflow](http://stackoverflow.com/questions/30386317/babelify-throws-parseerror-on-import-a-module-from-node-modules)

##  参考文档

http://www.w2bc.com/article/120144

https://github.com/substack/browserify-handbook
