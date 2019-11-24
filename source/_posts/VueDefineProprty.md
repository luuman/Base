title: Vue defineProperty 双向绑定详解
date: 2017-08-18 18:29:00
description:
categories:
- FrontFrame
tags:
- Vue
toc: true
author:
comments:
original:
permalink: 
---
　　**Vue组件探秘**双向绑定的实现方法有很多，今天我们来讲基于数据劫持的双向绑定。基于数据劫持的双向绑定有两种。`Object.defineProperty`与`proxy`,而VUE 3.0中使用的`proxy`
proxy 严格来说是代理，而非劫持。究竟什么优点让他代替了defineproperty。

框架 | 原理 | 方法
-----|------|----
KnockoutJS    | 基于观察者模式的双向绑定    | 
Ember    | 基于数据模型的双向绑定    | 
Angular    | 基于脏检查的双向绑定    | 
Vue    | 基于数据劫持的双向绑定   | Object.defineproperty
Vue    | 基于数据劫持的双向绑定   | proxy
Vue    | 基于数据劫持的双向绑定   | Object.observe（已废弃）

<!-- more -->



## 原理

Object.defineproperty

obj: 目标对象

prop: 需要操作的目标对象的属性名
descriptor: 描述符

return value 传入对象

```javascript
const obj = {}
Object.defineProperty(obj, 'text', {
	get: function() {
		console.log('get Val')
	},
	set: function(val) {
		console.log('set val:' + val)
		document.getElementById('p').innerHTML = val
	}
})
const input = document.getElementById('input')
input.addEventListener('keyup', function (e){
	obj.text = e.target.value
})
```

<main>
  <p>请输入:</p>
  <input type="text" id="input">
  <p id="p"></p>
</main>

<script type="text/javascript">
	(function () {
		const obj = {}
		Object.defineProperty(obj, 'text', {
			get: function() {
				console.log('get Val')
			},
			set: function(val) {
				console.log('set val:' + val)
				document.getElementById('p').innerHTML = val
			}
		})
		const input = document.getElementById('input')
		input.addEventListener('keyup', function (e){
			obj.text = e.target.value
		})
	})()
</script>


