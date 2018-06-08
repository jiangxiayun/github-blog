---
title: JS使用getComputedStyle()方法获取CSS属性值
date: 2018-06-08 10:39:22
tags: JavaScript
---
在对网页进行调试的过程中，经常会用到js来获取元素的CSS样式，方法有很多很多，现在仅把我经常用的方法总结如下：

1. `obj.style` 这个方法JS只能获取写在html标签中的写在style属性中的值（style=”…”），而无法获取定义在css里面的属性。

2. IE中使用的是`obj.currentStyle`方法，而FF是用的是`getComputedStyle` 方法
<!-- more -->

“DOM2级样式”增强了`document.defaultView`，提供了getComputedStyle()方法。
这个方法接受两个参数：要取得计算样式的元素和一个伪元素字符串（例如“:after”）。
如果不需要伪元素信息，第二个参数可以是null。
getComputerStyle()方法返回一个CSSStyleDeclaration对象，其中包含当前元素的所有计算的样式。

``` javascript
 var myDiv = document.getElementById("myDiv");
 var computedStyle = document.defaultView.getComputedStyle(myDiv, null);
 alert(computedStyle.backgroundColor); //"red"
 alert(computedStyle.width); //"100px"
 alert(computedStyle.height); //"200px"
 alert(computedStyle.border); //在某些浏览器中是“1px solid black”
```

边框属性可能也不会返回样式表中实际的border规则（Opera会返回，但其它浏览器不会）。存在这个差别的原因是不同浏览器解释综合属性的方式不同，因为设置这种属性实际上会涉及很多其他的属性。在设置border时，实际上是设置了四个边的边框宽度、颜色、样式属性。因此，即使computedStyle.border不会在所有浏览器中都返回值，但computedStyle.borderLeftWidth则会返回值。

需要注意的是，即使有些浏览器支持这种功能，但表示值的方式可能会有所区别。例如，Firefox和Safari会返回将所有颜色转换成RGB格式。因此，即使getComputedStyle()方法时，最好多在几种浏览器中测试一下。

IE不支持getComputedStyle()方法，但它有一种类似的概念。在IE中，每个具有style属性的元素还有一个currentStyle属性。这个属性是CSSStyleDeclaration的实例，包含当前元素全部计算后的样式。取得这些样式的方法差不多，如下：

```javascript
var myDiv = document.getElementById("myDiv");
var computedStyle = myDiv.currentStyle;
alert(computedStyle.backgroundColor); //"red"
alert(computedStyle.width); //"100px"
alert(computedStyle.height); //"200px"
alert(computedStyle.border); //undefined
```
与DOM版本的方式一样，IE也没有返回border样式，因为这是一个综合属性。


下面这个函数，能够获取一个元素的任意 CSS 属性值。

```javascript
function getStyle(element, attr) {
        if(element.currentStyle) {
                return element.currentStyle[attr];
        } else {
                return getComputedStyle(element, false)[attr];
        }
}
```

比如，本例中如果想获得 lists 的 left 属性值，只需要

 ```javascript
 getStyle(lists,"left")
 ```
