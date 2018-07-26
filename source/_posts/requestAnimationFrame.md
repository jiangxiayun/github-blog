---
title: requestAnimationFrame
date: 2018-06-19 13:50:54
tags: JavaScript
---

在做页面动画的时候，比如跑马灯，以前会用 setTimeout 、setInterval，但是为了更好的平稳过渡效果，现在会用 requestAnimationFrame 。特别是在 three.js 等3D鼠标交互页面中，requestAnimationFrame 是必备的。

<!-- more -->
设置这个API的目的是为了让各种网页动画效果（DOM动画、Canvas动画、SVG动画、WebGL动画）能够有一个统一的刷新机制，从而节省系统资源，提高系统性能，改善视觉效果。代码中使用这个API，就是告诉浏览器希望执行一个动画，让浏览器在下一个动画帧安排一次网页重绘。

requestAnimationFrame的优势，在于充分利用显示器的刷新机制，比较节省系统资源。显示器有固定的刷新频率（60Hz或75Hz），也就是说，每秒最多只能重绘60次或75次，requestAnimationFrame的基本思想就是与这个刷新频率保持同步，利用这个刷新频率进行页面重绘。此外，使用这个API，一旦页面不处于浏览器的当前标签，就会自动停止刷新。这就节省了CPU、GPU和电力。

不过有一点需要注意，requestAnimationFrame是在主线程上完成。这意味着，如果主线程非常繁忙，requestAnimationFrame的动画效果会大打折扣。

目前，主要浏览器Firefox 23 / IE 10 / Chrome / Safari）都支持这个方法。可以用下面的方法，检查浏览器是否支持这个API。如果不支持，则自行模拟部署该方法。
```javascript
window.requestAnimFrame = (function(){
  return  window.requestAnimationFrame       ||
    window.webkitRequestAnimationFrame ||
    window.mozRequestAnimationFrame    ||
    window.oRequestAnimationFrame      ||
    window.msRequestAnimationFrame     ||
    function( callback ){
      window.setTimeout(callback, 1000 / 60);
    };
})();
```
上面的代码按照1秒钟60次（大约每16.7毫秒一次），来模拟requestAnimationFrame。

requestAnimationFrame使用一个回调函数作为参数。这个回调函数会在浏览器重绘之前调用。使用requestAnimationFrame的时候，只需反复调用它即可。
```javascript
 function repeatOften() {
   // Do whatever
   requestAnimationFrame(repeatOften);
 }

 requestID = requestAnimationFrame(repeatOften);
```
cancelAnimationFrame方法用于取消重绘。
```javascript
 window.cancelAnimationFrame(requestID);
```

下面以我在vue项目里写的跑马灯为例，介绍 requestAnimationFrame 的使用
```javascript
  mounted () {
    this.wrap = document.getElementById('moveWarp')
    this.timer = requestAnimationFrame(this.move)  // 开始动画
    this.wrap.onmouseover = () => {
      window.cancelAnimationFrame(this.timer)   // 介绍动画
    }
    this.wrap.onmouseout = () => {
      if (!this.lastProcessShow) {
        this.timer = requestAnimationFrame(this.move)
      }
    }
  },
  methods: {
    move () {
      this.wrap.scrollTop++
      if (this.wrap.scrollTop >= this.wrap.scrollHeight - 65) {
        this.wrap.scrollTop = 0
      }
      this.timer = requestAnimationFrame(this.move)  // 循环动画
    }
  }
```