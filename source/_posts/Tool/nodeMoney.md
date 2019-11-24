title: 基金走势快查V1
date: 2017-10-27 14:11:20
description: 
categories:
- Node
tags:
- Node
toc: true
author:
comments:
original:
permalink: 
---
110011 | 2019-10-18 15:00 |        易方达中小盘混合  | -0.99
160127 | 2019-10-18 15:00 |    南方新兴消费增长分级  | -1.02
007490 | 2019-10-18 15:00 |       南方信息创新混合A  | -1.08
005919 | 2019-10-18 15:00 |        天弘中证500指数C | -1.28
000961 | 2019-10-18 15:00 |        天弘沪深300指数A | -1.35
001630 | 2019-10-18 15:00 | 天弘中证计算机主题指数C   | -1.69
001071 | 2019-10-18 15:00 |      华安媒体互联网混合  | -2.06
<!-- more -->

```javascript
var http = require('http')
var fundList = [
  // '003670', // 中融物联网主题灵活配置混合
  '001630', // 天弘中证计算机指数C
  '160127', // 南方新兴消费分级
  // '001938', // 中欧时代先锋股票A
  '000961', // 天弘沪深300指数
  // '340006', // 兴全全球视野股票
  '001071', // 华安媒体互联网混合
  // '001986', // 前海开源人工智能主题混合
  '005919', // 天弘中证500指数
  '007490', // 天弘中证500指数
  '110011', // 天弘中证500指数
]
function APIs(ID) {
  return new Promise((resolve, reject) => {
    http.get(`http://fundgz.1234567.com.cn/js/${ID}.js`, function (res) {
      var json = ''
      res.on('data', function (d) {
        json += d
      })
      res.on('end',function(){
        var item = JSON.parse(json.substr(8, json.length - 10))
        resolve(item)
      })
    }).on('error', function (e) {
      reject(e)
    })
  })
}
function logList(Array) {
  this.arr = Array
  var name = {}
  this.getByteLen = function (val) {
    var len = 0;
    for (var i = 0; i < val.length; i++) {
      var a = val.charAt(i)
      if (a.match(/[^\x00-\xff]/ig) != null) {
        len += 2
      }
      else {
        len += 1
      }
    }
    return len
  }
  var compare = function (sum1, sum2) {
    return sum2.gszzl - sum1.gszzl
  }
  this.arr.sort(compare)
  this.arr.forEach((item) => {
    for (var p in item) {
      if (name[p] == null) name[p] = 0
      item.len = this.getByteLen(item[p])
      if (name[p] < this.getByteLen(item[p])) {
        name[p] = this.getByteLen(item[p])
      }
    }
  })
  this.name = name
}
logList.prototype.debug = function(keys) {
  this.arr.forEach((item) => {
    var text = ''
    keys.forEach((p, index) => {
      var nbp = this.name[p] - this.getByteLen(item[p])
      while (nbp != 0) {
        text += ' '
        nbp--
      }
      text += item[p] + ((keys.length - 1 == index) ?  '' : ' | ')
    })
    console.log(text)
  })
}
var FundPros = new Promise((resolve, reject) => {
  var a = 0
  var Funds = []
  fundList.forEach((item) => {
    APIs(item).then((res) => {
      Funds.push(res)
      a++
      if (a >= fundList.length) {
        resolve(Funds)
      }
    })
  })
})
FundPros.then((res) => {
  var loggers = new logList(res)
  console.log(new Date())
  loggers.debug(['fundcode', 'gztime', 'name', 'gszzl'])
  console.log('done')
})
```
