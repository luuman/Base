title: 搜索历史
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

```javascript
function gohistroyList(item) {
  // 过滤重复项
  if (this.histroyList.includes(item)) {
    this.histroyList.splice(this.histroyList.indexOf(item), 1)
  }
  let History = []
  History.push(item)
  History = History.concat(this.histroyList)
  if (History.length > 11) History.splice(11, 1)
  this.histroyList = History
  localStorage.setItem('histroyList', JSON.stringify(this.histroyList))
}
```

```javascript
```
