---
title: 【微信小程序】JavaScript 从数组中删除指定值元素的方法封装
date:  2021-11-18 11:20:34
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 效果

```javascript
const somearray = ["mon", "tue", "wed", "thur"]
removeByValue(somearray, "tue");
//somearray will now have "mon", "wed", "thur"
```

## 方法

在 src/utils/util.js 中定义函数 `removeByValue` 进行元素删除：

```javascript
function removeByValue(arr, val) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === val) {
      arr.splice(i, 1);
      break;
    }
  }
}

module.exports = {
  removeByValue
};
```

然后在 src/pages/home/home.js 中引用：

```javascript
import util from '../../utils/util.js';
Page({

  /**
   * 页面的初始数据
   */
  data: {
	somearray: ['mon', 'tue', 'wed', 'thur']
  },

  /**
   * 删除数组某一值
   */
  delete: function (e) {
    const that = this;
    util.removeByValue(that.data.somearray, 'tue');
    console.log('somearray', that.data.somearray);
  },
  
  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    const that = this;
    that.delete();
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
});
```