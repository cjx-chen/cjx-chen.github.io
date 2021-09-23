---
title: 【微信小程序】下拉加载与上拉刷新
date: 2021-09-23 16:51:38
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 效果

![](https://img-blog.csdnimg.cn/8fb00676a4064837be9b9c049383e193.gif)

## 方法

1. 在 scroll-view 里设定 bindscrolltoupper 和 bindscrolltolower 实现微信小程序下拉；（本文使用此方法）
2. onPullDownRefresh和onReachBottom方法实现小程序下拉加载和上拉刷新；

## 代码

### index.wxml

```html
<scroll-view scroll-top="{{ scrollTop }}" scroll-y="true" style="height:{{ scrollHeight }}px; " class="list" bindscrolltolower="bindDownLoad" bindscrolltoupper="topLoad" bindscroll="scroll">
    <view class="article-block" wx:for="{{ ArticleList }}" wx:key="index" bindtap="gotoArticleDetail" data-articleid="{{ item.article_id }}">
      <view class="article-text">
        <view class="article-title">{{ item.title }}</view>
        <view class="article-time">{{ item.release_time }}</view>
      </view>
      <image class="article-image" src="{{ item.image }}"></image>
    </view>
    <view class="body-view">
     <loading hidden="{{hidden}}" bindchange="loadingChange">
       加载中...
     </loading>
   </view>
  </scroll-view>
```

### index.js

```javascript
const url = 'http://api/articlelist'
let page = 0
const pageSize = 5
const sort = 'last'
const isEasy = 0
const langeId = 0
const posId = 0
const unlearn = 0
// 请求数据
const loadMore = function(that) {
  that.setData({
    hidden: false
  })
  wx.request({
    url: url,
    data: {
      page: page,
      page_size: pageSize,
      sort: sort,
      is_easy: isEasy,
      lange_id: langeId,
      pos_id: posId,
      unlearn: unlearn
    },
    success: function(res) {
      // console.info(that.data.list);
      const list = that.data.ArticleList
      for (let i = 0; i < res.data.list.length; i++) {
        list.push(res.data.list[i])
      }
      that.setData({
        list: list
      })
      page++
      that.setData({
        hidden: true
      })
    }
  })
}

Page({
  /**
   * 页面的初始数据
   */
  data: {
    hidden: true,
    scrollTop: 0,
    scrollHeight: 0,
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
    ],
    value: '',
    offset: 0
  },
  
  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    const that = this
    wx.getSystemInfo({
      success: function (res) {
        that.setData({
          scrollHeight: res.windowHeight * 3 / 5
        })
      }
    })
    that.getSayings()
    that.getArticleList()
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

  },
  
  /**
   * 页面滑动到底部
   */
  bindDownLoad: function () {
    const that = this
    loadMore(that)
    console.log('lower')
  },

  /**
   * 页面滚动
   * @param {*} event
   */
  scroll: function (event) {
    // 该方法绑定了页面滚动时的事件，这里记录了当前的position.y的值,为了请求数据之后把页面定位到这里来。
    this.setData({
      scrollTop: event.detail.scrollTop
    })
  },

  /**
   * 上拉刷新
   * @param {*} event
   */
  topLoad: function(event) {
    //  该方法绑定了页面滑动到顶部的事件，然后做上拉刷新
    page = 0
    this.setData({
      ArticleList: [
        {
          article_id: 1,
          title: 'This is Title',
          release_time: '2020-03-12 09:42:19',
          image: 'https://img1.baidu.com/it/u=1001511637,3492134614&fm=26&fmt=auto&gp=0.jpg',
          text: 'This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. This is content of article. ',
          teacher_id: 1
        }
      ],
      scrollTop: 0
    })
    loadMore(this)
    console.log('lower')
  }
 })
```

### index.css

```css
/* 每日文章 */
.article-block{
  display: flex;
  height: 220rpx;
  width: 350rpx;
  margin: 0 50rpx 0 50rpx;
  padding: 20rpx 0 20rpx 0;
  border-top: 1px solid rgba(222, 222, 222, 0.5);
}

.article-text{
  position: absolute;
  flex: 1;
  height: 220rpx;
  width: 350rpx;
}

.article-title{
  position: absolute;
  top: 10rpx;
  font-size: 28rpx;
  padding-bottom: 10rpx;
}

.article-time{
  position: absolute;
  bottom: 0rpx;
  font-size: 22rpx;
  color: darkgrey;
  padding-bottom: 10rpx;
}

.article-image{
  position: absolute;
  right: 30rpx;
  width: 300rpx;
  height: 220rpx;
}
```

## 拓展

这里简单讲述一下另一种方法：

1. 首先要在 json 文件里设置 `window` 属性；
2. 设置 js 里 `onPullDownRefresh` 和 `onReachBottom` 方法；

下拉加载说明：
当处理完数据刷新后，`wx.stopPullDownRefresh` 可以停止当前页面的下拉刷新。

### 代码

```javascript
onPullDownRefresh(){
　　console.log('--------下拉刷新-------')
　　wx.showNavigationBarLoading() //在标题栏中显示加载
　　wx.request({
     url: 'https://URL',
     data: {},
     method: 'GET',
     // OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, CONNECT
     // header: {}, // 设置请求的 header
     success: function(res){
      // success
     },
     fail: function() {
      // fail
     },
     complete: function() {
      // complete
      wx.hideNavigationBarLoading() //完成停止加载
      wx.stopPullDownRefresh() //停止下拉刷新
   }
})
```