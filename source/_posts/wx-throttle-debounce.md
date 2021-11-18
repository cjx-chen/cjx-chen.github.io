---
title: 【微信小程序】使用函数防抖与函数节流
date:   2021-08-31 11:50:20
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
- 性能优化
- JavaScript
---

函数防抖和函数节流都是老生常谈的问题了。这两种方式都能优化 js 的性能。有些人可能会搞混两个的概念。

## 概念

### 函数防抖

**函数防抖**： 英文 debounce 有防反跳的意思，大致就是指防止重复触发。

那么，函数防抖，真正的含义是：延迟函数执行。即不管 debounce 函数触发了多久，只在最后一次触发 debounce 函数时，才定义 setTimeout，到达间隔时间再执行 需要防抖的函数。

**用处：多用于 input 框输入时，显示匹配的输入内容的情况。**

### 函数节流

**函数节流**： 英文 throttle 有节流阀的意思。大致意思也是 节约触发的频率

那么，函数节流，真正的含义是：单位时间 n 秒内，第一次触发函数并执行，以后 n 秒内不管触发多少次，都不执行。直到下一个单位时间 n 秒，第一次触发函数并执行，这个 n 秒内不管函数多少次都不执行。

**用处：多用于页面 scroll 滚动，或者窗口 resize，或者防止按钮重复点击等情况。**

---

其实如果只根据控制函数触发的频率是不好区分这两个概念的。我认为两个函数都能达到防止重复触发的功能。但是函数防抖是 n 秒后延迟执行；而函数节流是立马执行，n 秒后再立马执行。

## 方法封装

在小程序中，函数防抖、函数节流的使用方式：

一般都会把这两种方法封装在公用的 tool.js 中：

```javascript
/* 函数节流 */
function throttle(fn, interval) {
  let enterTime = 0 // 触发的时间
  const gapTime = interval || 300 // 间隔时间，如果interval不传，则默认300ms
  return function() {
    const context = this
    const backTime = new Date() // 第一次函数return即触发的时间
    if (backTime - enterTime > gapTime) {
      fn.call(context, arguments)
      enterTime = backTime // 赋值给第一次触发的时间，这样就保存了第二次触发的时间
    }
    console.log('节流成功!')
  }
}

/* 函数防抖 */
function debounce(fn, interval) {
  let timer
  const gapTime = interval || 1000 // 间隔时间，如果interval不传，则默认1000ms
  return function() {
    clearTimeout(timer)
    const context = this
    const args = arguments // 保存此处的arguments，因为setTimeout是全局的，arguments不是防抖函数需要的。
    timer = setTimeout(function() {
      fn.call(context, args)
    }, gapTime)
    console.log('防抖成功!')
  }
}

export default {
  throttle,
  debounce
}
```

##  方法调用

search-list.wxml：

```html
<!--pages/search-list/search-list.wxml-->
<!-- 顶部搜索框 -->
<van-search 
  focus="true"
  value="{{ value }}" 
  label="单词"
  placeholder="请输入搜索关键字" 
  shape="round"
  use-action-slot
  bind:search="onSearch"
  bind:change="onChange"
  clearable>
    <view slot="action" bind:tap="onClick">搜索</view>
</van-search>
```

search-list.json：

```json
"usingComponents": {
  "van-search": "@vant/weapp/search/index"
}
```

search-list.js：

```javascript
// pages/search-list/search-list.js

import tool from '../../utils/tool.js'

Page({

  /**
   * 页面的初始数据
   */
  data: {
    value: '',
    SearchList: []
  },

  /**
   * 检测搜索框输入
   */
  onChange: tool.debounce(function (msg) {
    // console.log(msg)
    console.log(msg[0].detail)
    this.setData({
      value: msg[0].detail,
      SearchList: []
    })
    this.getSearchList()
  }),

  /**
   * 按Enter搜索
   */
  onSearch: tool.throttle(function (msg) {
    console.log('搜索' + this.data.value)
    this.getSearchList()
  }),

  /**
   * 点击搜索
   */
  onClick: tool.throttle(function (msg) {
    // console.log('搜索' + this.data.value)
    this.setData({
      SearchList: []
    })
    this.getSearchList()
    if (this.data.value.trim() === '' || this.data.SearchList.length === 0) {
      wx.showToast({
        title: '查询不到该单词',
        icon: 'none'
      })
    }
  }),

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

实现效果如下：
![](https://img-blog.csdnimg.cn/faa75706fd4d4f90b76bf660e24ee1e5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Za15Za15Za15Za16KaB5oqx5oqx,size_20,color_FFFFFF,t_70,g_se,x_16)

## 区别说明

**函数节流的说明：**

1. 第一次执行时，是一定能执行函数的。

2. 然后，n 秒内第二次触发的时候，当第一次与第二次间隔不足设置的间隔时间时，就不会执行。之后第三、第四次触发还是不执行。

3. 直到 n 秒之后，有且仅有一次，并且是第一次再次触发函数。

**函数防抖的说明：**

1. 第一次触发函数时，定义了一个定时器。在 n 秒后执行。

2. 然后，函数第二次触发的时候，由于闭包的特性，这时候的 `timer` 已经是第一次触发时的 定时器的标识了。然后直接清除第一次的 `setTimeout`，这时候第一次的 `setTimeout` 里面的内容就不会执行了。然后再定义第二次的 `setTimeout`。

3. 然后重复第二个步骤，一直清除，又一直设置。直到函数最后一次触发，定义了最后的一个定时器，并且间隔 n 秒执行。

4. 如果在最后一个定时器没执行时，函数又触发了，那么又重复第三步。相当于设置的间隔时间，只是延迟函数执行的时间，而不是间隔多少秒再执行。


到这里，这两个方式的区别就很明显了。函数节流是减少函数的触发频率，而函数防抖则是延迟函数执行，并且不管触发多少次都只执行最后一次。