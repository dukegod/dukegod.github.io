---
title: 苹果下弹框问题
date: 2016-05-01
tags: CSS
---

## 弹框问题

把弹出框作为一个单独的层级提取出来。

最外层使用fixed属性，防止遮挡不全的问题。

最终解决方案：

  把body的高度设为100%，overflow：hidden


```
<<div class="mask"></div>
<div>
  body
</div>

.mask {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  bottom: 0;
  z-index: 9999;
  background: black;
  opacity: 0.3;
  -webkit-opacity: 0.2;
  display: none;
}
```

## 苹果下弹框问题

黑色背景框在一个层级，

内容在另一个层级

建议使用 absolute属性，解决iPhone手机遮挡不全的问题

否则活影响内部数据的显示与隐藏

控制body的样式，加上overflow：hidden属性
