title: js验证码实现方式
date: 2019-08-27 14:11:20
description: 
categories:
- JavaScript
tags:
- JavaScript
toc:
author:
comments:
original:
permalink: 
image: http://www.easyfinance.com.cn/Finance/images/Article/2019-02/21-09-50-55500711650_banner.jpg
---
　　**自用笔记：**搜索历史常见的功能
1. 添加搜索内容，有固定数量的显示
1. 重复添加位置替换
1. 到位添加数据
<!-- more -->

```
<button id="btn">获取验证码</button>
```

```javascript
var btn = document.getElementById("btn")
btn.onclick = function() {
	countDown(this)
}
function countDown(obj) {   //验证码60s倒计时
	var a = 10
	var timer = setInterval(tt,1000)
	function tt() {
		a--
		if ( a == 0 ) {
			obj.innerHTML = "重新获取"
			a = 60
			clearInterval(timer)
		} else {
			obj.innerHTML = a + 's'
		}
	}
}
```
