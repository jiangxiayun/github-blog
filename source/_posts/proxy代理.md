---
layout: vue
title: Vue 中 proxy代理
date: 2018-06-06 16:05:17
tags: Vue
thumbnail: https://example.com/image.jpg
---
Vue 框架开发的时候，会遇到跨域的问题，可在config/index.js 里配置proxyTable内容，使用proxy 代理。

<!-- more -->

```javascript
// config/index.js  文件
proxyTable: {
      '/api': {
        target: 'http://192.168.149.90:8080/', // 设置你调用的接口域名和端口号
        changeOrigin: true,     // 跨域
        pathRewrite: {
          '^/api': '/'
        }
      }
    },
```
这里理解成用‘/api’代替target里面的地址，后面组件中我们掉接口时直接用api代替 比如我要调用'http://192.168.149.90:8080/xxx/duty?time=2017-07-07 14:57:22'，直接写‘/api/xxx/duty?time=2017-07-07 14:57:22’即可

在dev.env.js 里配置开发环境请求地址

```javascript
// config/dev.env.js 文件
module.exports = merge(prodEnv, {
  NODE_ENV: '"development"',
  ADMIN_SERVER: '"/api/"',
});
```

若请求插件用的 axios，配置如下

```javascript
const adminServer = axios.create({
  baseURL: process.env.ADMIN_SERVER,
});
```

