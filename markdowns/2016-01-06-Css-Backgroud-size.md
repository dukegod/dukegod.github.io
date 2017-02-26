---
title: background-size
date: 2016-01-06
tags: CSS
---

支持情况：IE9+、Firefox 4+、Opera、Chrome 以及 Safari 5+  
在移动开发的时候，需要尺寸减半的需要。  
特别是在引入雪碧图的时候，以前的写法总是直接宽，高直接减半，没有出过问题

```
 .BZ{
    background:url() no-repeated;
    background-size: width/2, height/2;
}
```
<!--more-->

今天有人问我，background-size直接设为50%不就行了，没有细想，直接说行。

实际看效果的时候，出现了问题，原来不能这么用。

自己慢慢研究，先总结下：

先对照自己的例子说明下，增强自己的记忆：

[background-size  via @CodePen](http://codepen.io/dukegod/pen/YwGmXK)

#### background-size: 参考是元素本身的宽高，并不是参考引入图片的宽高,也就是说它参考的是section的大小，不是图片自身

直接缩减图片的宽高

```
.bz{
  background-image: url();
  background-repeat: no-repeat;
  background-size: 320px,200px;
}

```

#### 设置宽高一个属性的时候，另一个将会按照原来的比例进行变化(即设置一个属性，另一个等比例变化)

```
.bz{
  background-size: 320px,auto; // 高也会变半
  background-size: auto, 200px; // 宽也会变半
}
```

### 设置 100%，更好的适应各种分辨率

```
.bz{
  background-size: 100%,100%; // 承载更多的内容
}
```



### 设置多个背景图片

```
.secmul{
width: 480px;
height: 300px;
background-image: url(../../static/imgs/m1.jpg), url(../../static/imgs/m2.jpg), url(10.large.jpg);// set imgs urls
background-repeat: no-repeat,no-repeat,no-repeat;// set repeat pros
background-position: 0px 0px, right bottom, right top;// 设置不同的位置，相对与最外层的画布大小
background-color: #EEE;
background-size: 200px 225px, 100px 100px, cover;// 分别设置 不同背景图片的大小
}
```

#### cover与contain 属性详解

[background-size-prototype @CodePen](http://codepen.io/dukegod/pen/WrpLBp)

cover:背景图像缩放,保留图像原有的比例/长宽比,不管背景图像大于还是小于背景区域，都会覆盖背景区域,图像的宽度或高度等于或超过背景区域,再次,根据背景图像的比例是否匹配的背景区域,背景图像的某些部分可能不在背景区域内。

contain:背景图像缩放,同时保留图像原有的比例/长宽比,无论是图像的宽度或高度超过背景区域,以尽可能大的覆盖背景区域。因此,根据背景图像的比例是否匹配背景区域,可能会有一些背景图像覆盖不到背景地区。
