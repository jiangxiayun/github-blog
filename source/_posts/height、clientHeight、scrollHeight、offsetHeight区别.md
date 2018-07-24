---
title: height、clientHeight、scrollHeight、offsetHeight区别
date: 2018-07-24 15:53:30
tags:
---

![参数说明图](/images/height.gif)
<!-- more -->
### 1、偏移量：包括元素在屏幕上占用的所有可见空间（包括内边距、滚动条、边框大小）
![offset参数说明](/images/offset.jpg)
其中 offsetLeft 和 offsetTop 都与包含元素有关
```javascript
// 获取元素在页面上的偏移量
function getElementLeft(element){
  var actualLeft = element.offsetLeft;
  var current = element.offsetParent;
  while (current !== null){
    actualLeft += current.offsetLeft;
    current = current.offsetParent;
  }
  return actualLeft;
}

function getElementTop(element){
  var actualTop = element.offsetTop;
  var current = element.offsetParent;
  while (current !== null){
    actualTop += current. offsetTop;
    current = current.offsetParent;
  }
  return actualTop;
}
```

### 2、客户区大小：指的是元素内容及其内边距所占的空间大小（不包括滚动条和边框）
![client参数说明](/images/client.jpg)
```javascript
// 确定浏览器视口大小
function getViewport(){
  if (document.compatMode == "BackCompat"){
   // 混杂模式
    return {
      width: document.body.clientWidth,
      height: document.body.clientHeight
    };
  } else {
    return {
      width: document.documentElement.clientWidth,
      height: document.documentElement.clientHeight
    }; }
}
```


### 3、滚动大小：指的是包含滚动内容的元素的大小（不包括滚动条和边框）
![scroll参数说明](/images/scroll.jpg)
scrollWidth 和 scrollHeight 主要用于确定元素内容的实际大小
