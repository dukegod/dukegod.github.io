---
title: 修改github显示项目类型之gitattributes
date: 2017-02-07
tags: [Git, Github]
---
github 是根据项目里文件数目最多的文件类型,识别项目类型

如果需要修改项目类型解决办法:

在项目根目录添加 .gitattributes 文件

```
*.css linguist-language=javascript
*.js linguist-language=javascript
*.html linguist-language=javascript

```
