title: 移动端自适应Toast提示信息
date: 2015-12-25 18:29:00
description: 
categories:
- CSS
tags:
- CSS
toc: true
author:
comments:
original:
permalink: 
image: 
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。在此记录自己已理解并开始遵循的前端代码规范。What How Why
<!-- more -->



## 中文自动居中显示，自适应长度。
```CSS
position: fixed;
left: 50%;
top: 50%;
display: table;
max-width: 80%;
transform: translate(-50%,-50%);
```

## 纯英文，自动换行
```CSS
position: fixed;
left: 50%;
top: 50%;
max-width: 80%;
word-wrap: break-word;
transform: translate(-50%,-50%);
```
