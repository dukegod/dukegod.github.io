---
title:  zepto中操作option
date: 2016-02-01
tags: Zepto
---

zepto中操作option不能直接使用$('option:selected')。

需要使用$('option:checked')代替

或者使用如下代码

		$('option').not(function(){ return !this.selected })

