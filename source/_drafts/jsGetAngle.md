title:  js 计算获取鼠标相对某个点的移动旋转角度
date: 2019-05-27 14:11:20
description: 
categories:
- Induce
tags:
- JavaScript
toc:
author:
comments:
original:
permalink: 
---
　　** 自用笔记：**关于JS中比较常用的函数：节流函数和防抖函数，从概念、使用场景到代码简单实现做了一个详细的区分。希望对你有所帮助。What How Why
<!-- more -->

// 旋转角度
function getAngle(cen, first, second) {
	// cen  : 中心点 [0,0]
	// first : 开始点 [1,3]
	// second : 结束位置 [3,4]
  var f_c_x = first[0] - cen[0],
    f_c_y = cen[1] - first[1],
    s_c_x = second[0] - cen[0],
    s_c_y = cen[1] - second[1];
  var c = Math.sqrt(f_c_x * f_c_x + f_c_y * f_c_y) * Math.sqrt(s_c_x * s_c_x + s_c_y * s_c_y);
  if (c == 0) return -1;
  var angle = Math.acos((f_c_x * s_c_x + f_c_y * s_c_y) / c);
  // 第一象限
  if (cen[0] - second[0] < 0 && cen[1] - second[1] < 0) {
    return angle
    // 第二象限
  } else if (cen[0] - second[0] < 0 && cen[1] - second[1] > 0) {
    return angle
    // 第三象限
  } else if (cen[0] - second[0] > 0 && cen[1] - second[1] < 0) {
    return 2 * Math.PI - angle
    // 第四象限
  } else if (cen[0] - second[0] > 0 && cen[1] - second[1] > 0) {
    return 2 * Math.PI - angle
  }
}