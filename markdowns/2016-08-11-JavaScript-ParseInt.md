---
title: ParseInt
date: 2016-08-11
tags: [JavaScript]
---

函数将给定的字符串以指定基数解析成为整数。默认是以十进制为底数。    
会将传人的数据按照基数进行解析。

```
parseInt("546ddddd4444"); 
```

第一个为数字不是整数，返回为NAN

```
parseInt('i90')  // NAN
```

传人的参数不能被解析也报错

```
parseInt("546", 2);  // NAN
```
