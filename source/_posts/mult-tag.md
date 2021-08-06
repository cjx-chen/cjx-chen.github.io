---
title: 微信小程序 vant-weapp 实现多选标签
date: 2021-08-06 14:16:12
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 多选标签效果

![](https://img-blog.csdnimg.cn/28a9bcc0364b41bbac623f905592d8cf.gif)

## 配置 vant-weapp

步骤见：[https://jessieeeeee.xyz/2020/08/12/vantweapp-install/](https://jessieeeeee.xyz/2020/08/12/vantweapp-install/)

## demo.json

记得在 json 文件中引用 vant-weapp 的 tag 组件：

```json
{
  "usingComponents": {
    "van-tag": "@vant/weapp/tag/index"
  }
}
```

## demo.wxml

在 wxml 文件中搭建页面基础结构：

```html
<!--pages/demo/demo.wxml-->

<view>
  <view class="tagSelector">
    <view class="hot-search-tag">
      <block wx:for="{{ hotTag }}" wx:key="{{ index }}">
        <van-tag round color="{{ item.active?selectColor:tagBgColor }}" text-color="#333333" size="large" bindtap="itemSelected" data-index="{{ index }}">{{ item.tag }}
        </van-tag>
      </block>
    </view>
  </view>
</view>
```

## demo.wxss

在 wxss 文件中设置好基础样式：

```css
/* pages/demo/demo.wxss */

.tagSelector {
  text-align: left;
  font-size: larger;
  font-weight: bolder;
  margin: 40rpx 30rpx 40rpx 40rpx;
}

.hot-search-tag {
  margin-top: 20rpx;
}

.van-tag {
  margin: 10rpx 10rpx;
}

```

## demo.js

在 js 文件中定义数据及方法：

```javascript
// pages/demo/demo.js
Page({

  /**
   * 页面的初始数据
   */
  data: {
    tagBgColor: '#F5F5F5',
    selectColor: 'rgba(255,198,75,0.5)',
    hotTag: [{
        id: 1,
        tag: '春季穿搭',
        active: false
      },
      {
        id: 2,
        tag: '家常菜',
        active: false
      },
      {
        id: 3,
        tag: '文案',
        active: false
      },
      {
        id: 4,
        tag: '头像',
        active: false
      },
      {
        id: 5,
        tag: '健身',
        active: false
      },
      {
        id: 6,
        tag: '学习',
        active: false
      },
      {
        id: 7,
        tag: '美甲',
        active: false
      },
      {
        id: 8,
        tag: '装修',
        active: false
      },
      {
        id: 9,
        tag: '生日礼物',
        active: false
      },
      {
        id: 10,
        tag: '简笔画',
        active: false
      },
      {
        id: 11,
        tag: '电影',
        active: false
      },
      {
        id: 12,
        tag: '舞蹈',
        active: false
      }
    ]
  },

  /**
   * 选择标签
   */
  itemSelected: function (e) {
    let index = e.currentTarget.dataset.index;
    let item = this.data.hotTag[index];
    item.active = !item.active;
    this.setData({
      hotTag: this.data.hotTag,
    });
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {

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