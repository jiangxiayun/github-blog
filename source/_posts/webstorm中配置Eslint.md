---
title: webstorm中配置Eslint
date: 2018-06-19 13:28:50
tags: webstorm
categories: 开发工具相关
---
团队开发中，在代码规范这一块经常会用到Eslint，这篇文章主要介绍 webstorm中Eslint的配置
<!-- more -->
# 方式一：webstorm自带Eslint
用webstorm自带Eslint这种方式的话，只需要打开setting，找到eslint设置页面，填完几个项目，勾选enable复选框就行了。
`注意：`因为不同的项目可能使用的Eslint规范不一致，所以package这里指向项目里的Eslint安装包，
configuration file 指向项目里的 .eslintrc.js 文件

![webstorm-esline配置](/images/webstorm-eslint1.jpg)

## 使用方式
自带的使用方式是在左侧项目目录列表上，选中某个你想eslint自动修复的文件夹或文件，右键，会出现fix eslint problems菜单。如下图。
![webstorm-esline1](/images/webstorm-eslint2.png)
当然你也可以在右侧，代码编辑区域，选中某个要自动修复eslint监测出来有bug的文件，右键，点击fix eslint problems菜单。
可自行设置快捷键。


# 方式二：使用插件Eslint
这种方式呢，分两步，第一步：需要先到plugin插件库，找到eslint插件，点击install。如下图：
![webstorm-esline1](/images/webstorm-eslint3.png)


第二步：插件安装完成后，去setting页面，搜索eslint，这时你会发现，除了方式一那个eslint设置页面外，还多了一个设置页面，在setting对话框最下面的菜单。里面的设置项和方式一差不多。