---
title: vue迁移webpack4
date: 2018-09-11 11:10:24
tags: Vue webpack
categories: webpack
---
``` bash
(node:10768) DeprecationWarning: Tapable.plugin is deprecated. Use new API on `.hooks` instead
(node:10768) DeprecationWarning: Tapable.apply is deprecated. Call apply on the plugin directly instead



npm install extract-text-webpack-plugin@next --save-dev
```


vue-loader was used without the corresponding plugin. Make sure to include VueLoaderPlugin in your webpack config.

. Vue-loader在15.*之后的版本都是 vue-loader的使用都是需要伴生 VueLoaderPlugin的,

. 在webpack.config.js中加入

const VueLoaderPlugin = require('vue-loader/lib/plugin');

plugins: [
        // make sure to include the plugin for the magic
        new VueLoaderPlugin()
    ],