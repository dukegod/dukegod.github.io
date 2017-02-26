---
title:  事件委托
date: 2016-01-13
tags: JavaScript
---

事件委托就是事件本身不处理事件，把事件处理的任务托给其父亲或者祖先元素，甚至是根元素。

最常见的例子就是绑定li方法的委托事件。

<!--more-->

```
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
</ul>

(function(){
  $('body').on('click', 'li', function(event) {
    event.preventDefault();
    /* Act on the event */
    console.log(this);
  });
})(jQuery)
```

借用了jquery的on事件作为事件委托的方法。不介意使用bind方法。

原生方法可以用addEventListener方法进行绑定。





