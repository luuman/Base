title: 微信小程序之生成图片分享
date: 2019-07-27 14:11:20
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

　　**自用笔记：**由于人员问题，通常会有小程序内嵌WebView的需求。这里将整理讲解、注意事项。

<!-- more -->

promisify: api => {
  return (options, ...params) => {
    return new Promise((resolve, reject) => {
      const extras = {
        success: resolve,
        fail: reject
      }
      api({ ...options, ...extras }, ...params)
    })
  }
},


const wxGetImageInfo = this.promisify(wx.getImageInfo)

Promise.all([
    wxGetImageInfo({
        src: 'https://teststaticimage.yktour.com.cn/uploads/20190426/1215de9c5e8f5305289335ea10b4adab.jpg_360x240q80.jpg'
    }),
    wxGetImageInfo({
        src: 'https://teststaticimage.yktour.com.cn/uploads/20190426/1215de9c5e8f5305289335ea10b4adab.jpg_360x240q80.jpg'
    })
]).then(res => {
    const ctx = wx.createCanvasContext('shareCanvas')
    
    // 底图
    ctx.drawImage(res[0].path, 0, 0, 600, 900)

    // 作者名称
    ctx.setTextAlign('center')    // 文字居中
    ctx.setFillStyle('#000000')  // 文字颜色：黑色
    ctx.setFontSize(22)         // 文字字号：22px
    ctx.fillText('作者：一斤代码', 600 / 2, 500)

    // 小程序码
    const qrImgSize = 180
    ctx.drawImage(res[1].path, (600 - qrImgSize) / 2, 530, qrImgSize, qrImgSize)

    ctx.stroke()
    ctx.draw()
})



https://www.jianshu.com/p/ceb42fe76e77
https://www.jianshu.com/p/3056754987e8
https://www.jianshu.com/p/5f96a4f91b9c
https://developers.weixin.qq.com/miniprogram/dev/api/canvas/Canvas.html