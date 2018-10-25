---
title: 修改浏览器默认css
date: 2018-10-25 10:13:12
tags: css
categories: 意想不到的css
---
本文列出几种遇到过的，需要修改浏览器默认CSS样式的情况及解决方法：
* 修改input框placeholder的字体颜色
* 修改浏览器记住密码后输入框的背景色
<!-- more -->
------
### 1. 修改input框placeholder的字体颜色
``` css
       input::-webkit-input-placeholder, textarea::-webkit-input-placeholder {
         /* WebKit browsers */
         color: #6377B9;
       }
       input:-moz-placeholder, textarea:-moz-placeholder {
         /* Mozilla Firefox 4 to 18 */
         color: #6377B9;
       }
       input::-moz-placeholder, textarea::-moz-placeholder {
         /* Mozilla Firefox 19+ */
         color: #6377B9;
       }
       input:-ms-input-placeholder, textarea:-ms-input-placeholder {
         /* Internet Explorer 10+ */
         color: #6377B9;
       }
```
### 2. 修改浏览器记住密码后输入框的背景色
前言： 谷歌浏览器、在记住密码后，通常会给用户密码输入框渲染上一个背景色，
在有些时候这个浏览器自动使用的渲染背景色会影响系统本身的UI界面，所以下面提供css方法处理解决。
``` css
   /*处理浏览器输入框记住账号密码后的背景色*/
    input:-webkit-autofill, textarea:-webkit-autofill,
    select:-webkit-autofill {
      -webkit-text-fill-color: #ededed !important;
      -webkit-box-shadow: 0 0 0 1000px transparent inset !important;
      background-color: transparent;
      background-image: none;
      transition: background-color 50000s ease-in-out 0s;
      //背景色透明  生效时长  过渡效果  启用时延迟的时间
    }
    input {
      background-color: transparent;
    }
```