---
title: 前端开发字体研究
date: 2016-01-10
tags: [Font, App]
---

## 前端开发遇到的字体问题：

### 字体样式

#### 常见字体的中英文对照

sans-serif（无衬线），serif（衬线），monospace（等宽），fantasy（梦幻），cuisive（草体），Simsun（宋体），Microsoft Yahei（微软雅黑），Sim hei（黑体），STXihei（华文细黑）

#### 衬线体与无衬线体解释

+ Serif是“衬线体”，特点是笔画末端有装饰。中文字体中的“宋体”、“楷体”、“仿宋”都是衬线体。

+ Sans-serif是“无衬线体”，特点是笔画线条简单，末端没什么花哨的装饰。中文中的“黑体”“微软雅黑”就是这种字体。
无衬线体由于形状简单，容易矢量化，矢量化后的字体缩放不会出现锯齿，适合液晶屏显示。

+ monospace 字体，每个字母的宽度相等，通常用于计算机相关书籍中排版代码块。

+ fantasy 和 cuisive 字体在浏览器中不常用，在各个浏览器中有明显的差异。

#### 主要的字体分类

无衬线字体有：Arial、Helvetica、Lucida Grande、Verdana、Tahoma、Trebuchet MS Normal；

衬线字体有：Georgia、Times New Roman；

<!--more-->

### 各大手机供应商字体

#### iOS 系统

+ 默认中文字体是Heiti SC
+ 默认英文字体是Helvetica
+ 默认数字字体是HelveticaNeue
+ 无微软雅黑字体

#### Android 系统

+ 默认中文字体是Droidsansfallback
+ 默认英文和数字字体是Droid San
+ 无微软雅黑字体

#### Winphone 系统

+ 默认中文字体是Dengxian(方正等线体)
+ 默认英文和数字字体是Segoe
+ 无微软雅黑字体

各个手机系统有自己的默认字体，且都不支持微软雅黑,
**如无特殊需求，手机端无需定义中文字体,**
使用系统默认英文字体和数字字体可使用Helvetica种系统都支持。

```
body {
  font-family: "Helvetica Neue", Helvetica, STHeiTi, sans-serif;
}
```

### 移动端字体单位

+ em

em 的计算是基于父级元素的，在实际使用中给我们的计算带来了很大的不便

+ rem

基于根元素（html）

#### 如何使用

对于只需要适配手机设备，使用px即可

对于需要适配各种移动设备，使用rem，例如只需要适配iPhone和iPad等分辨率差别比较挺大的设备

设置转换(在rem前面，加上px，为了兼容性考虑的)

```
html{
	font-size:62.5%; /* 10/16=.625 */
}

body{
	font-size:12px;
	font-size:1.2rem ; /* 12/10=1.2 */
}

// body 中的字体也可以这么设置

body{
	font-size: 16px;
    font-size:1.6rem; // 设置全局的字体为16号
}

//需要设置html基础的字体大小，文档在加载的时候，按照html的样式进行渲染你也可以设置html
//字体的样式为其他的

html{
   font-size:32px;/*设置默认的字体大小*/
}
body{
  font-size: .5rem; /* 32*0.5= 16px */
}
```

rem加行media 进行响应式设计

```
html {font-size:10px}
@media screen and (min-width:480px) and (max-width:639px) {
    html {
        font-size: 15px
    }
}
@media screen and (min-width:640px) and (max-width:719px) {
    html {
        font-size: 20px
    }
}
@media screen and (min-width:720px) and (max-width:749px) {
    html {
        font-size: 22.5px
    }
}
@media screen and (min-width:750px) and (max-width:799px) {
    html {
        font-size: 23.5px
    }
}
@media screen and (min-width:800px) and (max-width:959px) {
    html {
        font-size: 25px
    }
}
@media screen and (min-width:960px) and (max-width:1079px) {
    html {
        font-size: 30px
    }
}
@media screen and (min-width:1080px) {
    html {
        font-size: 32px
    }
}
```

## 推荐资源

[国外人对于字体的研究**主要是英文啦**](http://ilovetypography.com/)

[中文排版的最佳实践](http://zhuanlan.zhihu.com/FrontendMagazine/19891152)

[]()

[The @Font-Face Rule And Useful Web Font Tricks](http://www.smashingmagazine.com/2011/03/02/the-font-face-rule-revisited-and-useful-tricks/)

[参考,更多的说明](http://www.asheep.cn/skill/web-mobile-o.html)

[计算字体的大小去适应(网易淘宝)](http://www.codeceo.com/article/font-size-web-design.html)
