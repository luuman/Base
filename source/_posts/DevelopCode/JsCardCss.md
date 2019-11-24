title: 翻转卡片
date: 2019-08-27 14:11:20
description:
categories:
- JavaScript
tags:
- JavaScript
toc: true
author: Hoang Nguyen
comments:
original:
permalink:
image: https://user-images.githubusercontent.com/10662852/65014472-69ac7900-d951-11e9-813c-75cbc049cab1.png
---
　　**CSS3动画探秘：**平时喜欢研究动效，下面来分析如何实现设计师的效果
[程序员追着打系列 by Hoang Nguyen](https://juejin.im/pin/5cdab976092dcb6246a7d1b2)
<!-- more -->

![](https://user-images.githubusercontent.com/10662852/65014472-69ac7900-d951-11e9-813c-75cbc049cab1.png)

<div class="anim">
	<div>☻</div>
</div>

<style type="text/css">
	@keyframes circle {
	  from { transform:rotate(-90deg); }
	  to { transform:rotate(90deg); }
	}
	@keyframes inner-circle {
	  from { transform:rotate(-90deg); }
	  to { transform:rotate(-270deg); }
	}
	.anim {
	  width:100px;
	  height:100px;
	  margin: 20px auto 0;
	  text-align: center;
	  color:orange;
	  font-size:100px;
	  line-height:1;
	  animation: circle 5s linear infinite;
	  transform-origin:50% 200px;
	}
	.anim > div {
	  animation: inner-circle 5s linear infinite;
	}
</style>

## 效果分析
1. 卡片移动距离
1. 旋转角度计算
1. 最大触电移动距离
1. 移动速度联动角度、距离的变化

由于只有效果图，数值只能靠肉眼感觉来调整。