---
title: 移动开发webkit
date: 2016-01-08
tags: [Webkit, App]
---

### -webkit-tap-highlight-color:rgba(255,255,255,0)

可以同时屏蔽ios和android下点击元素时出现的**阴影**。

备注：transparent的属性值在android下无效。

<!--more-->

###  -webkit-appearance:none

可以同时屏蔽输入框怪异的内阴影。

### -webkit-transform:translate3d(0, 0, 0)

在ios下可以让动画更加流畅（这个属性会调用硬件加速模式），但是在android下不可乱用，很多见所未见的bug就是因为这个。


###  -webkit-background-size

可以做高清图标，不过一些低版本的android只能识别background-size，所以有必要两个都要写上；用这个属性的时候推荐树勇cover这个值，可以自动去匹配宽和高。


###  -webkit-touch-callout: none;

长按时不触发系统的菜单, 可用在图片上加这个属性禁止下载图片;

亲测iOS可以，Android不支持

```
img{
-webkit-touch-callout: none;
}

```

### -webkit-user-select

不是标准属性

```
-webkit-user-select: none; //文档中不让文本选择
-webkit-user-select: text; //文档中只可以操作文本
-webkit-user-select: all;

```

### -webkit-text-size-adjust

主要是兼容Google对于字体的兼容性问题

当移动设备横竖屏切换时，文本的大小会重新计算，进行相应的缩放，当我们不需要这种情况时，可以选择禁止

需要注意的是，PC端的该属性已经被移除，该属性在移动端要生效，必须设置 meta viewport。

```
{
-webkit-text-size-adjust: 100%;
}
```

### -webkit-overflow-scrolling

在最外层添加这个属性，可以实现手机行接近原生的体验,可以在父级或者以上的父级添加添加这个属性就可以了

## 推荐资源

[webkit前缀(携程)](http://ued.ctrip.com/webkitcss/)

[mozilla_ webkit](https://developer.mozilla.org/en-US/docs/Web/CSS/Webkit_Extensions)
