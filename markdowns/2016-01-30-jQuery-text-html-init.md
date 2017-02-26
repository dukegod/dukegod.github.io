---
title:  jquery,zepto中的text,html,val深入理解
date: 2016-01-30
tags: [jQuery,Zepto]
---

### text，html，val共同点

val用来读取或修改表单元素的value值。

text用来读取或修改元素的纯文本内容

html用为读取和修改元素的HTML标签

<!--more-->

### 不同点

jquery中.htm()获取属性的HTML属性，**但是当使用在多个元素上时，只读取第一个元素**

jquery中.text()获取选取的内容的文本的时候，**当有多个元素的时候，读取所有的元素的text值**

zepto中的html()与text()方法在使用在多个元素的时候，**只读取第一个元素**

### trim()

原生方法，去除两边的空格。去检测获取的值是否为空的判断！

[演示代码](https://github.com/dukegod/h5-demos/tree/master/demos/jquery_text_html_val_trim)
