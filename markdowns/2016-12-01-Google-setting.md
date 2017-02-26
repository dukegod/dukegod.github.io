---
title: 谷歌使用总结
date: 2016-12-01
tags: [Google]
---

以开发者为导向的文档说明

## chrome://

#### chrome://version/

浏览器相关的信息

#### chrome://flags/

用来设置谷歌实验性的行功能，可以执行选择是否开启

+ enable-javascript-harmony : 允许网页使用实验性 JavaScript 功能,可以用来调试ES6新功能。
+ enable-point-point : 设为禁用，可以解决zepto报错的问题

####  chrome://extensions/

扩展插件控制

#### chrome://setting

设置

#### chrome://crashes/

崩溃报告，记录crash的具体id上报

## 谷歌浏览器设置

+ 字体 : 平-方


## 常用插件

+ Better History ：管理浏览器历史记录
+ Fast Video Downloader ：视频下载
+ HTTP/2 and SPDY indicator ：检测是不是启用了http2.0协议
+ JSON-handle
+ Markdown Editor
+ Octotree ： 用来管理github仓库，代码以树形结构显示
+ Proxy SwitchySharp ： 代理
+ React Developer Tools
+ Scratch JS ： ES6 代码书写
+ show ip
+ SoundCloud Music Downloader
+ Vue.js devtools
+ WEB前端助手(FeHelper)

## 常见问题

+ 在mac崩溃

```
sudo chown -R $USER ~/Library/Google
```

Thread 56 CRASHED [EXC_BAD_ACCESS / EXC_I386_GPFLT @ 0x000000010d16d6e4 ] MAGIC SIGNATURE THREAD 问题

It is related to Chrome Sync, so you may want to try signing out of Chrome sync and then logging back in. 意思是可能是因为同步的问题，清理日志与缓存重新登录下。
