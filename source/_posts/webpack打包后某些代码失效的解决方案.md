---
title: webpack打包后某些代码失效的解决方案
date: 2018-10-25 10:39:35
tags: webpack
categories: webpack
---
本文列出几种遇到过的，webpack打包代码后，某些功能或样式失效的情况及解决方案：
* 打包后丢失属性 -webkit-box-orient: vertical
<!-- more -->
------
### 1. 多行溢出省略的样式，打包后失效, -webkit-box-orient:vertical 丢失,解决方法如下
``` css
.omit {
  overflow:hidden;
  text-overflow: ellipsis;
  display:-webkit-box;
  -webkit-line-clamp:1;

  /*! autoprefixer: off */
  -webkit-box-orient: vertical; // 参考 https://github.com/postcss/autoprefixer/issues/776
  /* autoprefixer: on */

  /*解决打包后 -webkit-box-orient: vertical 丢失*/

}
```