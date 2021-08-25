---
title: 【微信小程序】实现新闻列表（文字垂直居上、垂直居下）
date: 2021-08-25 13:44:58
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 新闻列表效果
![](https://img-blog.csdnimg.cn/2542a861a6cb4cc4b98c820d7a043673.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_Q1NETiBA5Za15Za15Za15Za16KaB5oqx5oqx,size_11,color_FFFFFF,t_70,g_se,x_16)

## 相关原理
[CSS 的 absolute 定位](https://www.runoob.com/css/css-positioning.html)

值得注意的是，绝对定位的元素的位置相对于最近的**已定位**父元素，如果元素没有已定位的父元素，那么它的位置相对于`<html>`；

## 代码
### demo.wxml
```html
<!--pages/demo/demo.wxml-->

<view class="home-block">
  <!-- 每日文章 -->
  <view class="article-block" wx:for="{{ ArticleList }}" wx:key="index" bindtap="gotoArticleDetail" data-articleid="{{ item.article_id }}">
    <view class="article-text">
      <view class="article-title">{{ item.title }}</view>
      <view class="article-time">{{ item.release_time }}</view>
    </view>
    <image class="article-image" src="{{ item.image }}"></image>
  </view>
</view>
```
### demo.js

```javascript
// pages/demo/demo.js

Page({
  /**
   * 页面的初始数据
   */
  data: {
    ArticleList: [
      {
        article_id: 1,
        title: 'This is Title',
        release_time: '2020-03-12 09:42:19',
        image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
        text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
        teacher_id: 1
      },
      {
        article_id: 2,
        title: 'This is Title This is Title',
        release_time: '2020-03-12 09:42:19',
        image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
        text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
        teacher_id: 2
      },
      {
        article_id: 3,
        title: 'This is Title This is Title This is Title',
        release_time: '2020-03-12 09:42:19',
        image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
        text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
        teacher_id: 3
      },
      {
        article_id: 4,
        title: 'This is Title This is Title This is Title This is Title',
        release_time: '2020-03-12 09:42:19',
        image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
        text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
        teacher_id: 4
      }
    ]
  },

  /**
   * 进入文章详情界面
   */
  gotoArticleDetail: function (event) {
    // 当前要跳转到另一个界面，但是会保留现有界面
    wx.navigateTo({
      url: `../article-detail/article-detail?articleid=${event.currentTarget.dataset.articleid}`
    })
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
### demo.wxss
```css
/* pages/demo/demo.wxss */
.home-block {
  margin-bottom: 20rpx;
}

/* 每日文章 */
.article-block {
  display: flex;
  height: 220rpx;
  width: 350rpx;
  margin: 0 50rpx 0 50rpx;
  padding: 20rpx 0 20rpx 0;
  border-top: 1rpx solid rgba(222, 222, 222, 0.5);
}

.article-text {
  position: absolute;	/* 父元素绝对定位 */
  flex: 1;
  height: 220rpx;
  width: 350rpx;
}

.article-title {
  position: absolute;	/* 垂直居上 */
  top: 10rpx;	/* 垂直居上 */
  font-size: 28rpx;
  padding-bottom: 10rpx;
}

.article-time {
  position: absolute;	/* 垂直居下 */
  bottom: 0rpx;	/* 垂直居下 */
  font-size: 22rpx;
  color: darkgrey;
  padding-bottom: 10rpx;
}

.article-image {
  position: absolute;
  right: 30rpx;
  width: 300rpx;
  height: 220rpx;
}
```
### demo.json
```json
{
	"usingComponents": {}
}
```