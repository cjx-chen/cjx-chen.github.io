---
title: 【微信小程序】本地缓存保持登录状态之 wx.setStorageSync() 使用技巧
date: 2021-08-31 16:42:06
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
- 需求
tags:
- 微信小程序
- API
- JavaScript
---

## 简介

微信小程序提供了一个如同浏览器 cookie 本地缓存方法，就是 `wx.setStorageSync()` 。

注意，该方法是同步请求，还有个异步请求的方法是 `wx.setStorage()`，参考[官方文档](https://developers.weixin.qq.com/miniprogram/dev/api/storage/wx.setStorage.html)。

取出本地缓存方法 `wx.getStorageSync`，同样的，它也是同步请求，它也有一个异步请求方法 `wx.getStorage()`。

## 使用方法

登录时候，将所需要存的字段存入本地缓存中：

```javascript
// pages/daily/daily.js

// 获取本地缓存中的TOKEN
const TOKEN = wx.getStorageSync('TOKEN')

Page({
  data: {
    peopleDetails: []
  },

  /**
   * 获取每日人物信息
   */
  getCharacter() {
    // 发起网络请求
    wx.request({
      url: '<url>',
      method: 'get',
      header: {
        'content-type': 'application/json',
        Authorization: 'student ' + TOKEN
      },
      success(res) {
        console.log(res)
        if (res.code === 200) {
          this.setData({
            peopleDetails: this.data.peopleDetails.concat(JSON.parse(res.data))
          })
          console.log('peopleDetails', this.data.peopleDetails)
        } else {
          console.log('每日人物获取失败！', res.data.msg)
        }
      },
      fail(msg) {
        console.log(msg)
      }
    })
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    this.getCharacter()
  },

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady: function () {

  },

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {

  },

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {

  },

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload: function () {

  },

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh: function () {

  },

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom: function () {

  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage: function () {

  }
})
```