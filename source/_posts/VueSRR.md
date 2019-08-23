title: Vue SSR
date: 2018-08-25 18:29:00
description: 
categories:
- FrontFrame
tags:
- Vue
toc: true
author:
top: true
comments:
original:
permalink: 
image: http://img.zcool.cn/community/032bd3557a5abcd0000018c1b74486e.jpg
---
**服务器端渲染(Server-Side Rendering)：**
Vue.js 是构建客户端应用程序的框架。默认情况下，可以在浏览器中输出 Vue 组件，进行生成 DOM 和操作 DOM。然而，也可以将同一个组件渲染为服务器端的 HTML 字符串，将它们直接发送到浏览器，最后将静态标记"混合"为客户端上完全交互的应用程序。
服务器渲染的 Vue.js 应用程序也可以被认为是"同构"或"通用"，因为应用程序的大部分代码都可以在服务器和客户端上运行。
<!-- more -->

# 工作原理
![工作原理](https://user-gold-cdn.xitu.io/2018/5/24/16390509c83aef03?imageView2/0/w/1280/h/960/format/webp/ignore-error/1 "")

## app.js
app.js是我们的通用entry，它的作用就是构建一个Vue的实例以供服务端和客户端使用，注意一下，在纯客户端的程序中我们的app.js将会挂载实例到dom中，而在ssr中这一部分的功能放到了Client entry中去做了。

### Client entry.js
客户端的入口：功能很简单，就是挂载我们的Vue实例到指定的dom元素上
### Server entry.js
服务端的入口：一个使用export导出的函数。主要负责调用组件内定义的获取数据的方法，获取到SSR渲染所需数据，并存储到上下文环境中。这个函数会在每一次的渲染中重复的调用。

# 双刃剑
## 优点
### 更利于SEO
不同爬虫工作原理类似，只会爬取源码，不会执行网站的任何脚本（Google除外，据说Googlebot可以运行javaScript）。使用了Vue或者其它MVVM框架之后，页面大多数DOM元素都是在客户端根据js动态生成，可供爬虫抓取分析的内容大大减少。另外，浏览器爬虫不会等待我们的数据完成之后再去抓取我们的页面数据。服务端渲染返回给客户端的是已经获取了异步数据并执行JavaScript脚本的最终HTML，网络爬中就可以抓取到完整页面的信息。

### 更利于首屏渲染
首屏的渲染是node发送过来的html字符串，并不依赖于js文件了，这就会使用户更快的看到页面的内容。尤其是针对大型单页应用，打包后文件体积比较大，普通客户端渲染加载所有所需文件时间较长，首页就会有一个很长的白屏等待时间。

## 缺点
### 服务端压力较大
本来是通过客户端完成渲染，现在统一到服务端node服务去做。尤其是高并发访问的情况，会大量占用服务端CPU资源；

### 开发条件受限
在服务端渲染中，created和beforeCreate之外的生命周期钩子不可用，因此项目引用的第三方的库也不可用其它生命周期钩子，这对引用库的选择产生了很大的限制；

### 学习成本相对较高
1. webpack要熟悉
1. Vue要熟悉
1. 掌握node、Express相关技术，相对于客户端渲染，项目构建、部署过程更加复杂。

``` javascript
```