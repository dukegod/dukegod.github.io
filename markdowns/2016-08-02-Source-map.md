---
title: sourceMap
date: 2016-08-02
tags: [开发工具]
---

在前端优化中，普遍采用压缩文件的方式来减少文件体积提高加载速度，但是这个办法也有一定的坏处，比如：在调试程序是不能很好地定位追踪，而且阅读也很困难    
针对上述问题，google为我们提供了Source Maps这一解决方案.

Source Map 提供了连接生产环境代码和原始代码的方式。其实 Source Map就是一个信息文件存储了位置信息也就是存了压缩后代码的每一个位置所对应的压缩前的位置。   
Source Map文件内容是 JSON 格式的。当代码出错后，浏览器会根据Source Map加载.map文件，然后直接将错误信息定位到压缩前的代码。

Chrome和FireFox提供了很好地支持。不过在Chrome中默认是没有开启的，要在开发人员工具箱中设置一下，勾选Enalbe source maps。

### 解决Source Map跨域问题

那我们把js文件调用地址修改为127.0.0.1来测试一下跨域，经测试发现Source Map在跨域下不可用。   

那解决办法自然我们就行到了HTML5中的crossorigin。在引用js的script标签上添加crossorigin，再来看是什么样子，这次又可以正确的提示代码的信息了

在Apache中如何添加响应头？

1、检查是否开启了LoadModule headers_module modules/mod_headers.so，没有开启的话在配置文件中将这句前面的#去掉。

2、在<Directory />下添加Header set Access-Control-Allow-Origin="*"。

3、重启服务，然后刷新页面，看看Response Headers中是否有Access-Control-Allow-Origin:*。

在Apache中添加header响应头可以再<Directory>, <Location>, <Files> , <VirtualHost> , .htaccess中添加。

语法：

Header set 响应头 "取值"
帮助地址：mod_headers

在Apache中如何添加响应类型？

1、打开mime.types这个配置文件。

2、按照格式添加即可。比如：application/map json。

### 代码实现

css实现sourcemap功能

```
gulp.task('scss', function() {
  return gulp.src('./src/scss/pages/*.scss')
    .pipe(sourcemaps.init())
    .pipe(sass({ style: 'expanded' }).on('error', sass.logError))
    // .pipe(gulp.dest('dist/css'))
    .pipe(autoprefixer({
      browsers: ['ios 4', 'ios 5', 'ios 6', 'android 4', 'android 2.2', 'Safari 6', 'Safari 7'],
      cascade: false
    }))
    .pipe(cleanCSS())
    .pipe(sourcemaps.write('.'))
    .pipe(gulp.dest('dist/css'))
    .pipe(reload({ stream: true }));
});
```
sourcemaps.init() 方法一定要放在源码以后。  

sourcemaps.write(): 控制输出的文件

+ sourcemaps.write('.')；这么配置输出的为 xxx.map结尾
+ sourcemaps.write('./map'); 输出到文件中


### 总结

1、Source Map 使我们可以更有好的调试代码。

2、Source Map 可以定位到源文件中的行数。但是使用window.onerror是不能正确捕获错误发生的行号的。

3、Source Map 不支持跨域。

4、并不是所有浏览器都支持Source Map。

## 参考

http://www.cnblogs.com/fsjohnhuang/p/4208566.html

http://wanbei.github.io/2016/03/01/go-go-go-source-map/
