---
title: requestAnimationFrame
date: 2018-06-19 13:50:54
tags: JavaScript
---

在做页面动画的时候，比如跑马灯，以前会用 setTimeout 、setInterval，但是为了更好的平稳过渡效果，现在会用 requestAnimationFrame 。特别是在 three.js 等3D鼠标交互页面中，requestAnimationFrame 是必备的。
下面以我在vue项目里写的跑马灯为例，介绍 requestAnimationFrame 的使用
<!-- more -->
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