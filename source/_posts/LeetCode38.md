title: LeetCode 报数
date: 2019-07-27 14:11:20
description: 
categories:
- LeetCode
tags:
- LeetCode
toc: true
author:
comments:
original:
permalink: 
image: 
---
　　**自用笔记：**报数序列是指一个整数序列，按照其中的整数的顺序进行报数，得到下一个数。其前五项如下：
1.     1
2.     11
3.     21
4.     1211
5.     111221
<!-- more -->

```javascript
function showNum (num, n = 1) {
  let funss = (m,n)=> Array.apply(null,new Array(m)).map(()=>n++)
  let arr = funss(num, n)
  arr.forEach((arrA, key) => {
  	if (key) {
		  let arrY = String(arr[key - 1]).split('')
		  let arrB = []
			arrY.filter((item, index) => {
				if (index && item == arrY[index - 1]) {
					arrB[arrB.length - 1] += item
				} else {
					arrB.push(item)
				}
			})
			arr[key] = arrB.map(item => `${item.length}${item.slice(0, 1)}`).join('')
  	}
  })
  return arr[num - 1]
}
console.log(showNum(10))
```

```javascript
function showNum(key) {
	let Arr = new Array(key).fill('').map((item, index) => String(index + 1));
	Arr.reduce((ArrA, ArrB) => {
		let redA = ArrA == 1 ? '11' : ArrA.split('').reduce((arrC, arrD) => {
			return arrC.length - 1 == 0 ? arrC == arrD ? `2${arrD}` : `1${arrC}1${arrD}` : arrC.slice(arrC.length - 1, arrC.length) == arrD ? `${arrC.slice(0, arrC.length - 2 > 0 ? arrC.length - 2 : 0)}${+arrC.slice(arrC.length - 2, arrC.length - 1) + 1}${arrD}` : `${arrC}1${arrD}`
		})
		console.log("ArrB", ArrB, redA)
		return redA
	})
}
showNum(10)
```
