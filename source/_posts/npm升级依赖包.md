---
title: npm升级依赖包
date: 2018-07-26 13:27:45
tags: npm
---

使用npm管理node的包，可以使用npm update <name>对单个包升级


[npm-check](https://www.npmjs.com/package/npm-check)是用来检查npm依赖包是否有更新，错误以及不在使用的，我们也可以使用npm-check进行包的更新。

<!-- more -->

安装npm-check：
``` bash
npm install -g npm-check
```
检查npm包的状态：
``` bash
npm-check -u -g
```

通过上下键可以移动光标，使用空格键可以选择需要处理的包，回车直接进行处理。


[npm升级所有的依赖包](https://www.jianshu.com/p/a33702a4b096)