---
title: Safari不能把事件绑定到body上
date: 2017-01-06
tags: [Hack]
---

ios开发不能把事件绑定到body上  

也就是说，window，document，body 绑定click事件时，点击body不会触发，是Safari中的坑，所有的ios设备都是这样。

解决方案：

```
<body>
  <div id="ios">

  </div>
</body>

$('#ios').on()

```

绑定到最近的父一级的DOM
