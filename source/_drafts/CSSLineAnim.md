title: 大胆尝试 点与线动效设计
date: 2019-08-27 14:11:20
description:
categories:
- JavaScript
tags:
- JavaScript
toc: true
author: Vitaly Silkin
comments:
original:
permalink:
image: https://user-gold-cdn.xitu.io/2018/12/14/167ab6481f292cb1?imageView2/2/w/800/q/85
---
　　**CSS3动画探秘：**平时喜欢研究动效，下面来分析如何实现设计师的效果

<!-- more -->

[点与线动效设计——作者：Vitaly Silkin](https://juejin.im/pin/5c134cfb092dcb2cc5de73ad)

### 运动的小球
<div class="anim">
  <div class="ani colr1"></div>
  <div class="ani colr2"></div>
  <div class="ani colr3"></div>
  <div class="ani colr4"></div>
  <div class="ani colr5"></div>
</div>
<style type="text/css">
  .anim{
    position: relative;
    width: 389px;
    margin: auto;
    padding: 39px;
  }
  .ani{
    width: 40px;
    height: 40px;
    border-radius: 40px;
    float: left;
    margin-right: 20px;
    transition: background 0.5s;
  }
  .colr1{
    animation: colr1 5s infinite cubic-bezier(0.02, 0.01, 0.21, 1);
    opacity: 1;
  }
  .colr2{
    background: #ff6f22;
    animation: colr2 5s infinite cubic-bezier(0.02, 0.01, 0.21, 1);
  }
  .colr3{
    background: #ff4c41;
    animation: colr3 5s infinite cubic-bezier(0.02, 0.01, 0.21, 1);
  }
  .colr4{
    background: #ff2265;
    animation: colr4 5s infinite cubic-bezier(0.02, 0.01, 0.21, 1);
  }
  .colr5{
    background: #ff0a79;
    animation: colr5 5s infinite cubic-bezier(0.02, 0.01, 0.21, 1);
  }
  @keyframes colr1{
    0%{
      background: #ff9206;
    }
    12.5%{
      background: #ff6f22;
      transform: translate(60px);
    }
    25%{
      background: #ff4c41;
      transform: translate(120px);
    }
    37.5%{
      background: #ff2265;
      transform: translate(180px);
    }
    50%{
      background: #ff0a79;
      transform: translate(240px);
    }
    62.5%{
      background: #ff2265;
      transform: translate(180px);
    }
    75%{
      background: #ff4c41;
      transform: translate(120px);
    }
    87.5%{
      background: #ff6f22;
      transform: translate(60px);
    }
    100%{
      background: #ff9206;
    }
  }
  @keyframes colr2{
    0%{
      transform:rotate(0deg);
      transform-origin: 20px 0px;
    }
    6.25%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    12.5%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    25%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    37.5%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    50%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    62.5%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    75%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    87.5%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    93.75%{
      transform:rotate(0deg);
      transform-origin: 20px 0px;
    }
    100%{
    }
  }
  @keyframes colr3{
    0%{
    }
    6.25%{
    }
    12.5%{
      transform:rotate(0deg);
      transform-origin: 20px 0px;
    }
    25%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    37.5%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    50%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    62.5%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    75%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    87.5%{
      transform:rotate(0deg);
      transform-origin: 20px 0px;
    }
    93.75%{
    }
    100%{
    }
  }
  @keyframes colr4{
    0%{
    }
    6.25%{
    }
    12.5%{
    }
    25%{
      transform:rotate(0deg);
      transform-origin: 20px 0px;
    }
    37.5%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    50%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    62.5%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    75%{
      transform:rotate(0deg);
      transform-origin: 20px 0px;
    }
    87.5%{
    }
    93.75%{
    }
    100%{
    }
  }
  @keyframes colr5{
    0%{
    }
    6.25%{
    }
    12.5%{
    }
    25%{
    }
    37.5%{
      transform:rotate(0deg);
      transform-origin: 20px 0px;
    }
    50%{
      transform:rotate(-360deg) translate(-60px);
      transform-origin: -30px -20px;
    }
    62.5%{
      transform:rotate(0deg);
      transform-origin: 20px 0px;
    }
    75%{
    }
    87.5%{
    }
    93.75%{
    }
    100%{
    }
  }
</style>
<!-- ![](https://user-gold-cdn.xitu.io/2018/12/14/167ab6481f292cb1?imageView2/2/w/800/q/85) -->

### 的

<!-- ![](https://user-gold-cdn.xitu.io/2018/12/14/167ab64a078c1b61?imageView2/2/w/800/q/85) -->

<!-- ![](https://user-gold-cdn.xitu.io/2018/12/14/167ab61b964f8e88?imageView2/2/w/800/q/85) -->
<!-- ![](https://user-gold-cdn.xitu.io/2018/12/14/167ab6342943249a?imageView2/2/w/800/q/85) -->
<!-- ![](https://user-gold-cdn.xitu.io/2018/12/14/167ab636a699522b?imageView2/2/w/800/q/85) -->
<!-- ![](https://user-gold-cdn.xitu.io/2018/12/14/167ab63e197e7b50?imageView2/2/w/800/q/85) -->
<!-- ![](https://user-gold-cdn.xitu.io/2018/12/14/167ab6405c9ddd7e?imageView2/2/w/800/q/85) -->
<!-- ![](https://user-gold-cdn.xitu.io/2018/12/14/167ab64371daa12b?imageView2/2/w/800/q/85) -->
<!-- ![](https://user-gold-cdn.xitu.io/2018/12/14/167ab6463ec75554?imageView2/2/w/800/q/85) -->
