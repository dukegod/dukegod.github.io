---
title: node 通信之 socket
date: 2016-04-15
tags: [Node,JavaScript]
---

socket是一个WebSocket库，包括了客户端的js和服务器端的nodejs，它的目标是构建可以在不同浏览器和移动设备上使用的实时应用。

### socket.io特点

- 易用性：socket.io封装了服务端和客户端，使用起来非常简单方便。
- 跨平台：socket.io支持跨平台，这就意味着你有了更多的选择，可以在自己喜欢的平台下开发实时应用。
- 自适应：它会自动根据浏览器从WebSocket、AJAX长轮询、Iframe流等等各种方式中选择最佳的方式来实现网络实时应用，非常方便和人性化，而且支持的浏览器最低达IE5.5。
