---
title: 谷歌插件开发总结
date: 2016-03-15
tags: [JavaScript,Google]
---

谷歌插件开发，网上有很多的参考资源，开发的本质还是自己动手，即使开发最简单的功能，也能体验其中的原委。

这次开发一个“回到顶部”的功能，因为有的时候浏览一起网页，并没有置顶的功能，影响浏览体验。简述开发过程（带完善）

<!-- more -->

1, 创建一个manifest.json文件，用来存放你具体的项目的各种配置

2, 创建一个background.js入口

3, 创建一个html文本

4, 创建一个icon(可以省略)

5, 这样你就可以创建一个应用，想加载到浏览器中进行浏览，你可以打开：谷歌浏览器扩展中心，点击“加载已解压的扩展程序”，然后就可以在标签栏中预览你的插件功能了。

最终就是按照web开发方式去开发了，你可以选择web开发方式随意发挥你的才华了。

具体的代码托管在github

[on-click-top](https://github.com/dukegod/chrome-extension-add-top)


### 推荐阅读

[谷歌开发文档360](http://open.chrome.360.cn/extension_dev/overview.html)
[谷歌开发文档](https://developer.chrome.com/webstore/get_started_simple)
[app介绍](https://developer.chrome.com/apps/about_apps)
[谷歌应用发布](https://chrome.google.com/webstore/developer/dashboard)
