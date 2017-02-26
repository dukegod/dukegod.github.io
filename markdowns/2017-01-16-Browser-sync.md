---
title:  browser-sync
date: 2017-01-16
tags: [JavaScript]
---
[中文文档](http://www.browsersync.cn/)

[官方文档](https://browsersync.io/)

能够在本地服务器启动完成时自动帮我们打开浏览器，并且在相应的 jade，livescript，scss 文件改变时自动刷新浏览器.

[browsersync 与 liveload的比较的慕课视频](http://www.imooc.com/learn/718)

```
var gulp = require('gulp');
var browserSync = require('browser-sync').create();
var reload      = browserSync.reload;
gulp.task('browsersync', function() {
    browserSync.init({
        server: './dist'，
        proxy: '',
        // 选择在哪个浏览器打开
        browser:'',
        port:

    });
    gulp.watch('dist/*.html').on('change', reload);
});
```
