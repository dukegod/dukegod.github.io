---
title: node中buffer
date: 2016-11-05
tags: [Node]
---

对于JavaScript来说，对Unicode编码的数据很容易处理的但是对于二进制数据就没什么处理方法了。
但是在一些TCP数据流或者在操作一些文件数据流的时候，字节流的处理方法还是必须的。
nodeJS中便出了处理的策略方法~提供了与String类似对等的全局构造函数Buffer（与其说与String对等，还不如说与Array类似但是有些不同方面还是需要注意），
全局那么自然就不要每次的require了。Buffer则node中储存二进制数据的中介者。

https://www.15yan.com/story/gn1nYZr6hUQ/
