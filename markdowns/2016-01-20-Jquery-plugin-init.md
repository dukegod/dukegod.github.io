---
title:  jQuery插件开发
date: 2016-01-20
tags: jQuery
---

就我自己喜欢开发的模式，总结下jquery插件开发需要注意点。
主要是扩展jquery原型，防止变量污染；

<!--more-->

自己喜欢的开发模式：

```
;
(function($) {
$.fn.taptrace = function(options) {
	var defauts = {
		bgcolor: 'blue',
		timeLasting: '20'
	}
	if (options) {
		$.extend(defauts, options);
	}

	var $el = this;
	var events = 'ontouchstart' in window ? ['touchstart', 'touchmove touchend touchcancel'] : ['mousedown', 'mousemove mouseup'];
	var timer;
	var start = function() {
		if (timer) {
			return false;
		}
		timer = window.setTimeout(function() {
			$el.css('background-color', defauts.bgcolor);
		}, 5)
	}

	var stop = function() {
		window.clearTimeout(timer);
		timer = null;
		setTimeout(function() {
			$el.css('background-color', '');
		}, defauts.timeLasting)
	}
	$el.on(events[0], start);
	$el.on(events[1], stop);
}
})(jQuery)

```

1： ;最外面的分号是为了预防别人代码因为没有结束，带来的影响

2： 封装在闭包里面，防止代码的污染

3：default放在自己是放在属性里面进行引入的，也可以提出放在最外层

4： $.extend(defauts, options); 扩展默认值

调用

```
$('.pure-css').taptrace({
bgcolor:'red',
timeLasting:'10'
});
```

[项目地址](https://github.com/dukegod/jqueryTapTrace)

## 推荐阅读

[jQuery插件开发的模式和结构](http://www.cnblogs.com/cyStyle/archive/2013/05/18/jQuery%E6%8F%92%E4%BB%B6%E8%AF%A6%E7%BB%86%E5%BC%80%E5%8F%91.html)
