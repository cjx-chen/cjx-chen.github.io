---
title: 【微信小程序】上传头像
date:  2021-11-07 17:00:16
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
- 需求
tags:
- 微信小程序
- API
- JavaScript
---

## 效果
![](https://img-blog.csdnimg.cn/c987f59478c84802b2abd04224414358.gif)

## 代码
### editInfo.js
```javascript
// pages/editInfo/editInfo.js

Page({

  /**
   * 页面的初始数据
   */
  data: {
    dataList: []
  },

  /**
   * 获得图片本地路径
   */
  chooseWxImage: function () {
    const that = this;
    wx.chooseImage({
      // 最多可以选择的图片张数
      count: 1,
      // 所选的图片的尺寸
      sizeType: ['original', 'compressed'],
      // 选择图片的来源
      sourceType: ['album', 'camera'],
      success: function (res) {
        wx.showToast({
          title: '正在上传...',
          icon: 'loading',
          mask: true,
          duration: 10000
        });
        console.log(res);
        console.log(res.tempFilePaths[0]);
        that.upImgs(res.tempFilePaths[0], 0); // 调用上传方法
      },
      fail: function (res) {
        console.log('fail', res);
      },
      complete: function (res) {

      }
    });
  },

  /**
   * 上传服务器
   * @param {*} imgurl
   * @param {*} index
   */
  upImgs: function (imgurl, index) {
    const that = this;
    wx.uploadFile({
      url: `http://api`,
      // 小程序本地的路径
      filePath: imgurl,
      // 后台获取我们图片的key
      name: 'file',
      header: {
        'content-type': 'multipart/form-data'
      },
      // 额外的参数formData
      formData: {},
      success: function (res) {
        const datas = JSON.parse(res.data);
        console.log(datas);
        if (datas.code === 1) {
          wx.setStorageSync('PROFILEURL', 'http://' + datas.data);
          const profileUrl = wx.getStorageSync('PROFILEURL');
          that.setData({
            profileUrl: profileUrl
          });
          wx.showToast({
            title: '头像上传成功',
            icon: 'success',
            duration: 2000,
            mask: true,
            success: res => {}
          });
          console.log('success', res); // 接口返回网络路径
        } else {
          wx.showModal({
            title: '错误提示',
            content: datas.message,
            showCancel: false,
            success: function (res) { }
          });
          console.log('fail', datas.message);
        }
      },
      fail: function (res) {
        console.log('fail', res);
        wx.hideToast();
        wx.showModal({
          title: '错误提示',
          content: '上传图片失败',
          showCancel: false,
          success: function (res) { }
        });
      }
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
});
```
### profile.js

```javascript
// pages/profile/profile.js

// 获取本地缓存
const USERID = wx.getStorageSync('USERID');
const ROLEID = wx.getStorageSync('ROLEID');
const PROFILEURL = wx.getStorageSync('PROFILEURL');
const NICKNAME = wx.getStorageSync('NICKNAME');
const POSTNUM = wx.getStorageSync('POSTNUM');
const FANSNUM = wx.getStorageSync('FANSNUM');
const INTRODUCE = wx.getStorageSync('INTRODUCE');
const TAGLIST = wx.getStorageSync('TAGLIST');

Page({

  /**
   * 页面的初始数据
   */
  data: {
    UserInfo: [{
      profileUrl: PROFILEURL,
      nickname: NICKNAME,
      postNum: POSTNUM,
      fansNum: FANSNUM,
      introduce: INTRODUCE,
      tagList: TAGLIST
    }],
    pageNum: 1,
    userPageSize: 4,
    personalId: USERID,
    userId: USERID,
    onRefresh: false,
    roleId: ROLEID
  },

  /**
   * 刷新普通用户信息
   * @param {*} event
   */
  updateUserInfo: function () {
    // 获取本地缓存
    const PROFILEURL = wx.getStorageSync('PROFILEURL');
    const NICKNAME = wx.getStorageSync('NICKNAME');
    const POSTNUM = wx.getStorageSync('POSTNUM');
    const FANSNUM = wx.getStorageSync('FANSNUM');
    const INTRODUCE = wx.getStorageSync('INTRODUCE');
    const TAGLIST = wx.getStorageSync('TAGLIST');
    // 更新缓存
    const that = this;
    for (let i = 0; i < that.data.UserInfo.length; i++) {
      // console.log(that.data.UserInfo.length);
      const profileUrl = 'UserInfo[' + i + '].profileUrl';
      const nickname = 'UserInfo[' + i + '].nickname';
      const postNum = 'UserInfo[' + i + '].postNum';
      const fansNum = 'UserInfo[' + i + '].fansNum';
      const introduce = 'UserInfo[' + i + '].introduce';
      const tagList = 'UserInfo[' + i + '].tagList';
      that.setData({
        [profileUrl]: PROFILEURL,
        [nickname]: NICKNAME,
        [postNum]: POSTNUM,
        [fansNum]: FANSNUM,
        [introduce]: INTRODUCE,
        [tagList]: TAGLIST
      });
    }
    // console.log(that.data.UserInfo[0].profileUrl);
  },

  /**
   * 跳转编辑资料界面
   */
  gotoEditInfo: function (event) {
    // 当前要跳转到另一个界面，但是会保留现有界面
    wx.navigateTo({
      url: `../editInfo/editInfo?${this.data.dataList}`
    });
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    const that = this;
    if (USERID === 0) {
      wx.redirectTo({ url: 'pages/login/login' });
    }
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
    // 每次回到这个页面都要更新缓存
    const that = this;
    if (ROLEID === 1) {
      that.updateUserInfo();
    } else {
      wx.showToast({
        title: '用户未登录！', // 提示的内容,
        icon: 'none', // 图标,
        duration: 2000, // 延迟时间,
        mask: true, // 显示透明蒙层，防止触摸穿透,
        success: res => {}
      });
      console.log('用户未登录！');
    }
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