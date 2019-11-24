title: 小程序实现卡片
date: 2019-06-27 14:11:20
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
　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。在此记录自己已理解并开始遵循的前端代码规范。What How Why
<!-- more -->



### 返回顶部及获取滑动距离

```wx
<!-- 组件 -->
<card-sroll wx:if="{{List.length}}" catch:cancelAdd="cardAdd" catch:cancelCut="cardCut"></card-sroll>
```

```wx
<!-- 组件 -->
<view class="sroll">
  <view class="container container1" wx:if="{{page == 1}}" bindtouchstart="touchStart" bindtouchmove="touchMove" bindtouchend="touchEnd" animation="{{ani1}}">
    121212
  </view>
  <view class="container container2" wx:if="{{page == 2}}"  bindtouchstart="touchStart" bindtouchmove="touchMove" bindtouchend="touchEnd" animation="{{ani2}}">
    121212
  </view>
  <view class="container container3" wx:if="{{page == 3}}"  bindtouchstart="touchStart" bindtouchmove="touchMove" bindtouchend="touchEnd" animation="{{ani3}}">
    1212121
  </view>
</view>
```

```wx
.container{
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 0 25rpx;
  box-sizing: border-box;
}
.container1{
}
.container2{
}
.container3{
}
page{
  height: 100%
}
```

属性 | 说明
---|---
touchStart  | 触摸开始事件
touchMove   | 触摸移动事件
touchEnd    | 触摸结束事件
clientX     | 触摸目标在视口中的x坐标。
clientY     | 触摸目标在视口中的y坐标。
force       |
identifier  | 标识触摸的唯一ID。
pageX       | 触摸目标在页面中的x坐标。
pageY       | 触摸目标在页面中的y坐标。
move2left   | 向左滑动操作
move2right  | 向右滑动操作
screenX     | 触摸目标在屏幕中的x坐标。
screenY     | 触摸目标在屏幕中的y坐标。

```wx
const app = getApp()
var startX, endX;
var moveFlag = true;// 判断执行滑动事件

Component({
  data: {
    page : 1,
    ani1: '',
    ani2: '',
    ani3: ''
  },
  touchStart (e) {
    startX = e.touches[0].pageX; // 获取触摸时的原点
    moveFlag = true;
  },
  // 触摸移动事件
  touchMove (e) {
    endX = e.touches[0].pageX; // 获取触摸时的原点
    if (moveFlag) {
      if (endX - startX > 50) {
        console.log("move right");
        this.move2right();
        moveFlag = false;
      }
      if (startX - endX > 50) {
        console.log("move left");
        this.move2left();
        moveFlag = false;
      }
    }
  },
  // 触摸结束事件
  touchEnd (e) {
    moveFlag = true; // 回复滑动事件
  },
  //向左滑动操作
  move2left () {
    let {page, navTab, bottomList} = this.data
    var that = this
    if (page == bottomList.length) {
      return
    }
    var animation = wx.createAnimation({
      duration: 1000,
      timingFunction: 'ease',
      delay: 100
    });
    animation.opacity(0.2).translate(-500, 0).step()
    this.setData({
      ani1: page == 1 ? animation.export() : '',
      ani2: page == 2 ? animation.export() : ''
    })
    setTimeout(function () {
      that.setData({
        page: page + 1,
        ani3: '',
        ani2: ''
      });
    }, 800)
    this.triggerEvent('cancelAdd', page)
  },
  //向右滑动操作
  move2right () {
    let {page, navTab, bottomList} = this.data
    var that = this
    if (page == 1) {
      return
    }
    var animation = wx.createAnimation({
      duration: 1000,
      timingFunction: 'ease',
      delay: 100
    });
    animation.opacity(0.2).translate(500, 0).step()
    this.setData({
      ani3: page == 3 ? animation.export() : '',
      ani2: page == 2 ? animation.export() : ''
    })
    setTimeout(function () {
      that.setData({
        page: page - 1,
        ani1: '',
        ani2: ''
      });
    }, 800)
    this.triggerEvent('cancelCut', page)
  }
})
```

```wx
```


```wx
```

