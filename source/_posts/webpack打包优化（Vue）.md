---
title: webpack打包优化（Vue）
date: 2018-09-10 11:20:00
tags: webpack vue
---
1. 注意 devtool 中的 source-map。
如果你打包后的文件莫名其妙的好几 MB的大小, 那不用想了肯定是 source-map 的问题, 注意 source-map 的那种几种类型使用.
建议在production环境打包的时候关闭 devtool.

如果非得在线上使用 source-map, 可以配置为

devtool: "#source-map",
2. 使 css 剥离 js 文件, 将 css 单独打包。
依赖插件 npm install --save-dev extract-text-webpack-plugin 先安装再使用
``` bash
var ExtractTextPlugin = require('extract-text-webpack-plugin');
    
    //在 plugins 中配置
    plugins: [ new ExtractTextPlugin('[name].[contenthash].css') ]
```
把 css 单独打包出来，免得以后只修改 css 导致 浏览器端 js 的缓存也失效了。
这里使用了 contenthash, webpack 会按照内容去生成 hash 值。
3. 压缩, 去除注释

``` bash
//在 plugins 中添加
    new webpack.optimize.UglifyJsPlugin({
        comments: false,        //去掉注释
        compress: {
            warnings: false    //忽略警告,要不然会有一大堆的黄色字体出现……
        }
    })
```
