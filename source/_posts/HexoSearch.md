title:  Hexo 添加搜索功能
date: 2019-07-27 18:29:00
description: 
categories:
- Hexo
tags:
- Hexo
toc: true
author:
comments:
original:
permalink: 
image: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1566291945991&di=ab1879c0517bcdf2c8e840becefe32b2&imgtype=0&src=http%3A%2F%2Fi0.hdslb.com%2Fbfs%2Farchive%2F037b0052bd6dca74b8e46727e86d8e16c32316c3.png
---
　　** Hexo 主题：最为静态页面最为鸡肋的就是没有搜索功能，查找文件夹十分困难。第三方插件不稳定。今天就来实现内部功能。
<!-- more -->
## 插件

### hexo-generator-json-content搜索功能
jsonContent:
  meta: false
  pages: false
  posts:
    title: true
    date: true
    path: true
    text: false
    raw: false
    content: true
    slug: true
    updated: false
    comments: true
    link: false
    author: true
    permalink: true
    excerpt: false
    categories: true
    tags: true

插件会自动生成content.json文件，对文件数据进行查询。

## 动态获取数据

``` Javascript
// 动态获取数据
$('#local-search-input').bind('input propertychange', e => {
  let val = $('#local-search-input').val()
  if (window.history && window.history.pushState) val ? history.pushState({}, 'jsdig', '?search=' + val) : history.pushState({}, 'jsdig', '/')
  searchTool.searchGo(val)
})
```

``` Javascript
var searchTool = {
  data: [],
  arrList: [],
  oldList: [],
  init () {
    this.fetchJson()
  },
  fetchJson () {
    window.fetch(CONFIG.root + 'content.json?t=' + (+ new Date()), {
      method: 'get',
    }).then((res) => {
      console.log(res)
      return res.json()
    }).then((data) => {
      console.log(data)
      this.data = data
      this.searchList()
    }).catch((err) => {
      console.log(err)
    });
  },
  // 搜索字符串里面是否存在关键字
  isSreachIndexOF (oldstr, kw) {
    // console.log(oldstr, kw)
    var istrue = false
    // console.log('isSreachIndexOF', oldstr && toString.call(oldstr) === '[object Array]')
    if (oldstr && toString.call(oldstr) === '[object Array]') {
      for (var i = 0; i < oldstr.length; i++) {
        oldstr[i].toLowerCase() === kw.toLowerCase() ? istrue = true : null
      }
      return istrue
    }
    // console.log('isSreachIndexOF', !oldstr, !kw)
    if (!oldstr || !kw) return false
    istrue = oldstr.toLowerCase().indexOf(kw.toLowerCase()) > -1
    return istrue
  },
  searchList () {
    let divList = ''
    this.data.forEach(item => {
      divList += `
      <li>
        <a href="/${item.path}" class="search-result-title">${item.title}</a>
        <div class="main">
          <p class="left">
            <span>${item.author ? item.author : 'Luuman'}</span>
            ${item.tags.map(tags => `<a href="/tags/${tags.slug}" class="search-result-tags">${tags.name}</a>`)}
          </p>
          <p class="right">${this.getFriendlyTime(item.date.replace('T', ' '), new Date())}</p>
        </div>
      </li>`
    })
        // <p class="search-content">${item.content}</p>
    $('.search-result-list').html(divList)
  },
  clear () {
    this.oldList.forEach(item => {
      $(".search-result-list li")[item].style.display = 'none'
    })
    this.oldList = []
  },
  add () {
    this.arrList.forEach(item => {
      $(".search-result-list li")[item].style.display = 'block'
    })
    this.oldList = this.arrList
  },
  searchGo (keywolds) {
    this.arrList = []
    if (!keywolds) {
      if (this.oldList.length) this.clear()
    } else {
      this.data.forEach((item, index) => {
        if (this.isSreachIndexOF(item.title, keywolds) || this.isSreachIndexOF(item.tags.map(item => item.name).join('-'), keywolds) || this.isSreachIndexOF(item.categories.map(item => item.name).join('-'), keywolds) || this.isSreachIndexOF(item.content, keywolds)) {
          this.arrList.push(index)
        }
      })
      if (this.oldList.length) this.clear()
      if (this.arrList.length) this.add()
    }
  },
  /**
   * 获取指定时间的友好时间字符串。
   * @param str 指定的时间字符串，如yyyy-MM-dd HH:mm:ss
   * @param now 当前时间，允许时间戳，GMT时间，如果该参数为undefined，则使用浏览器时间。
   */
  getFriendlyTime (str, now) {
    var currentTime = new Date(now);
    var arr = str.split(/\s+/gi);
    var temp = 0, arr1, arr2, oldTime, delta;
    var getIntValue = function(ss, defaultValue){
      try{
        return parseInt(ss, 10);
      }catch (e){
        return defaultValue;
      }
    };
    var getWidthString = function(num){
      return num < 10 ? ('0' + num) : num;
    };
    if(arr.length >= 2){
      arr1 = arr[0].split(/[\/\-]/gi);
      arr2 = arr[1].split(':');
      oldTime = new Date();
      oldTime.setYear(getIntValue(arr1[0], currentTime.getFullYear()));
      oldTime.setMonth(getIntValue(arr1[1], currentTime.getMonth() + 1) - 1);
      oldTime.setDate(getIntValue(arr1[2], currentTime.getDate()));

      oldTime.setHours(getIntValue(arr2[0], currentTime.getHours()));
      oldTime.setMinutes(getIntValue(arr2[1], currentTime.getMinutes()));
      oldTime.setSeconds(getIntValue(arr2[2], currentTime.getSeconds()));

      delta = currentTime.getTime() - oldTime.getTime();

      if (delta <= 60 * 1000) {
        return '1分钟内';
      } else if (delta < 60 * 60 * 1000) {
        return Math.floor(delta / (60 * 1000)) + '分钟前';
      } else if (delta < 24 * 60 * 60 * 1000) {
        return Math.floor(delta / (60 * 60 * 1000)) + '小时前';
      } else if (delta < 24 * 60 * 60 * 1000 * 30) {
        return Math.floor(delta / (24 * 60 * 60 * 1000)) + '天前';
      } else if (delta < 24 * 60 * 60 * 1000 * 30 * 12) {
        return Math.floor(delta / (24 * 60 * 60 * 1000 * 30)) + '月前';
      } else if (currentTime.getFullYear() != oldTime.getFullYear()){
        return [getWidthString(oldTime.getFullYear()), getWidthString(oldTime.getMonth() + 1), getWidthString(oldTime.getDate())].join('-')
      } else {
        return [getWidthString(oldTime.getMonth() + 1), getWidthString(oldTime.getDate())].join('-');
      }
    }
    return '';
  }
}
console.log('err')
searchTool.init()
```
