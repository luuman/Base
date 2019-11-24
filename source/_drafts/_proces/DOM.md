# DOM 事件

## DOM 事件级别
DOM0 element.onclick = function () {}

DOM1 没有关于事件的内容

DOM2 element.addEventListener('click', function () {}, false)
定义事件

DOM3 element.addEventListener('keyup', function () {}, false)
事件类型增加了很多（鼠标、键盘）

## DOM 事件模型
事件模型：捕获和冒泡

### 兼容性
1）、所有现代浏览器都支持事件冒泡，但在具体实现中略有差别：

IE5.5及更早版本中事件冒泡会跳过<html>元素(从body直接跳到document)。

IE9、Firefox、Chrome、和Safari则将事件一直冒泡到window对象。

2）、IE9、Firefox、Chrome、Opera、和Safari都支持事件捕获。尽管DOM标准要求事件应该从document对象开始传播，但这些浏览器都是从window对象开始捕获事件的。

3）、由于老版本浏览器不支持，很少有人使用事件捕获。建议使用事件冒泡。

## DOM 事件流
DOM标准规定事件流包括三个阶段：事件捕获阶段、处于目标阶段和事件冒泡阶段。

### 事件捕获阶段
实际目标（<div>）在捕获阶段不会接收事件。也就是在捕获阶段，事件从document到<html>再到<body>就停止了。上图中为1~3.

### 处于目标阶段
事件在<div>上发生并处理。但是事件处理会被看成是冒泡阶段的一部分。

### 冒泡阶段
事件又传播回文档。

### 注意：
1. window => document => html => body => 
		window => document => document.documentElement => document.body => 
> Event常见的使用

event.preventDefault() 阻止默认
event.stopPropagation() 阻止冒泡
event.stopImmediatePropagation() 事件响应优先级

event.currentTarget 绑定的节点
event.target 捕获到的监听节点

可以通过绑定
## DOM 事件流流程

## Event对象的常见应用

addEventLi

## 自定义事件



