---
title: js小技巧集合
date: 2018-07-26 13:22:27
tags: JavaScript
---
<!-- more -->

 1、去除字符串中的特殊符号
 思路：正则表达式匹配

```javascript
var a="今天是星期五，  明天又可以放假了&好好休|息一下"
var b=a.replace(/[&\|\\\*^%$#@\-]/g,"");
alert(b);
```