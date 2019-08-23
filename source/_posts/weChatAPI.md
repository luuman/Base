title: 小程序知识点总结
date: 2019-08-27 14:11:20
description: 
categories:
- WeChat
tags:
- WeChat
toc: true
author:
comments:
original:
permalink: 
image: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1566382029281&di=2dc28d99e5c1c6dd82d616841b7f5ce7&imgtype=0&src=http%3A%2F%2Fhomesitetask.zbjimg.com%2Fhomesite%2Ftask%2Fd9c347.png%2Forigine%2F1dd2fcc6-1152-48db-861e-958bf99c3cd7
---

　　**AJAX：**Asynchronous Javascript And XML（异步JavaScript和XML）。是指一种创建交互式网页应用的网页开发技术。 AJAX = 异步 JavaScript和XML（标准通用标记语言的子集）。 AJAX 是一种用于创建快速动态网页的技术。 通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。 传统的网页（不使用 AJAX）如果需要更新内容，必须重载整个网页页面。

<!-- more -->

## Page
page()函数注册页面

属性 | 类型  | 说明
---|---|---
data | Object |  页面的初始数据
onLoad | function |  生命周期回调—监听页面加载
onShow | function |  生命周期回调—监听页面显示
onReady| function |  生命周期回调—监听页面初次渲染完成
onHide | function |  生命周期回调—监听页面隐藏
onUnload | function |  生命周期回调—监听页面卸载
onPullDownRefresh| function |  监听用户下拉动作
onReachBottom| function |  页面上拉触底事件的处理函数
onShareAppMessage| function |  用户点击右上角转发
onPageScroll | function |  页面滚动触发事件的处理函数
onResize | function |  页面尺寸改变时触发，详见 响应显示区域变化
onTabItemTap | function |  当前是 tab 页时，点击 tab 时触发
其他 | any |  开发者可以添加任意的函数或数据到 Object 参数中，在页面的函数中用 this 可以访问

```wx
//index.js
Page({
  data: {
    text: "This is page data."
  },
  onLoad: function(options) {
    // 页面创建时执行
  },
  onShow: function() {
    // 页面出现在前台时执行
  },
  onReady: function() {
    // 页面首次渲染完毕时执行
  },
  onHide: function() {
    // 页面从前台变为后台时执行
  },
  onUnload: function() {
    // 页面销毁时执行
  },
  onPullDownRefresh: function() {
    // 触发下拉刷新时执行
  },
  onReachBottom: function() {
    // 页面触底时执行
  },
  onShareAppMessage: function () {
    // 页面被用户分享时执行
  },
  onPageScroll: function() {
    // 页面滚动时执行
  },
  onResize: function() {
    // 页面尺寸变化时执行
  },
  onTabItemTap(item) {
    // tab 点击时执行
    console.log(item.index)
    console.log(item.pagePath)
    console.log(item.text)
  },
  // 事件响应函数
  viewTap: function() {
    this.setData({
      text: 'Set some data for updating view.'
    }, function() {
      // this is setData callback
    })
  },
  // 自由数据
  customData: {
    hi: 'MINA'
  }
})
```

### 下拉刷新
`onPullDownRefresh () {}` 触发下拉刷新时执行

下拉效果
enablePullDownRefresh
```wx
{
  "enablePullDownRefresh": true //当前页
  "backgroundTextStyle": "dark" //顶部显示颜色为深色的三个点
}

"window": {
  "enablePullDownRefresh": true //全局
  "backgroundTextStyle": "dark" //顶部显示颜色为白色的三个点
}
```

```wx
onPullDownRefresh: function () {
  var that = this;
  that.setData({
    currentTab: 0 //当前页的一些初始数据，视业务需求而定
  })
  this.onLoad(); //重新加载onLoad()
},
onLoad: function (options) {
  wx.stopPullDownRefresh() //刷新完成后停止下拉刷新动效
  //后面的业务代码大家自行发挥
},
```

### 下拉刷新
`onPullDownRefresh () {}` 触发下拉刷新时执行

```wx
onReachBottom () {
  console.log('onReachBottom')
  wx.showLoading({
    title: '玩命加载中',
  })
},

<!-- 关闭弹窗 -->
wx.hideLoading()
```

## API
### 动态设置顶部导航栏的背景色

wx.setNavigationBarTitle(OBJECT)

属性 | 变量 | 必传 | 解释
---|---|---|---
title | 类型：String | 必填：是 | 说明：页面的标题
success | 类型：Function | 必填：否 | 说明：接口调用成功的回调函数
fail | 类型：Function | 必填：否 | 说明：接口调用失败的回调函数
complete | 类型：Function | 必填：否 | 说明：接口调用结束的回调函数（调用成功或失败都会执行）

```wx
wx.setNavigationBarTitle({
  title: 'title'
})
```

### 动态设置顶部导航栏的背景色

属性 | 变量 | 必传 | 解释
---|---|---|---
fontColor | String | 是 | 前景颜色值，包括按钮、标题、状态栏的颜色，仅支持`#fff`和`#000`
backgroundColor | String | 是 | 背景颜色,有效值为16进制颜色
animation | Object | 否 | 动画效果
animation.duration | Number | 否 | 动画变化时间，默认0，单位（毫秒）
animation.timingFunc | String | 否 | 动画变化方式，默认`linear`
success | Function | 否 | 接口调用成功的回调函数
fail | Function | 否 | 接口调用失败的回调函数
complete |  Function | 否 | 接口调用结束的回调函数（成功、失败都会执行）

```wx
wx.setNavigationBarColor({
  frontColor: '#ffffff',
  backgroundColor: '#ff0000'
})
```

```wx
wx.setNavigationBarColor({
  frontColor: '#ffffff',
  backgroundColor: '#ff0000',
  animation: {
    duration: 400,
    timingFunc: 'easeIn'
  }
})
```

### 滑动监听

```wx
onPageScroll: function(res) {
  console.log(res)
},
// {scrollTop: 14}
```

### 返回顶部及获取滑动距离

```wx
//返回顶部
  goScrolltop:function(e){
    if (wx.pageScrollTo) {
      wx.pageScrollTo({
        scrollTop: 0
      })
    } else {
      wx.showModal({
        title: '提示',
        content: '当前微信版本过低，无法使用该功能，请升级到最新微信版本后重试。'
      })
    }
  },
```

## 组件开发
Component 构造函数

```wx
Component({
  behaviors: [],
  properties: {
    myProperty: { // 属性名
      type: String,
      value: ''
    },
    myProperty2: String // 简化的定义方式
  },
  data: {}, // 私有数据，可用于模板渲染
  lifetimes: {
    // 生命周期函数，可以为函数，或一个在methods段中定义的方法名
    attached: function () { },
    moved: function () { },
    detached: function () { },
  },
  // 生命周期函数，可以为函数，或一个在methods段中定义的方法名
  attached: function () { }, // 此处attached的声明会被lifetimes字段中的声明覆盖
  ready: function() { },
  pageLifetimes: {
    // 组件所在页面的生命周期函数
    show: function () { },
    hide: function () { },
    resize: function () { },
  },
  methods: {
    onMyButtonTap: function(){
      this.setData({
        // 更新属性和数据的方法与更新页面数据的方法类似
      })
    },
    // 内部方法建议以下划线开头
    _myPrivateMethod: function(){
      // 这里将 data.A[0].B 设为 'myPrivateData'
      this.setData({
        'A[0].B': 'myPrivateData'
      })
    },
    _propertyChange: function(newVal, oldVal) {
    }
  }
})
```


### swiper

[swiper](https://developers.weixin.qq.com/miniprogram/dev/component/swiper.html "")

