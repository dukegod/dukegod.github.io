---
title:  express 中间件笔记
date: 2016-04-04
tags: Node
---

最初产生于中间件，然后才有了express。

express 3.x版本依赖于connect中间件，connect中间件有22个内置的中间件可以运用。  
express 4.x不是依赖connect中间件，需要自行下载

### 中间件挂载:

```
app.use()
```

#### 默认的中间，用来处理静态文件，express.static()

```
app.use(express.static(path.join(__dirname, './public/')));
```

#### 自定义中间件

验证登陆，加密处理，通过next()继承中间件   
默认'/'可以省略掉

```
app.use('/',function(req, res, next) {
  var err = new Error('Not Found');
  err.status = 404;
  next(err);
});
```
#### 常用的中间件

+ morgan : 处理日志记录
+ body-parser : 处理POST方式提交的数据，放回到body中，得到数据'req.body'
+ cookie-parser : 用来解析cookie，服务器解析给浏览器中的数据
+ session-parser : 处理session
+ serve-favicon ： 处理网站图标
