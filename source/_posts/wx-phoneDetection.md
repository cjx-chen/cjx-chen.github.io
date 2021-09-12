---
title: 【微信小程序】判断手机号是否合法
date: 2021-09-12 13:07:03
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 场景
在注册页面输入手机号，在请求注册接口前先行判别输入的手机号码是否合法；

## 效果
![注册界面样式](https://img-blog.csdnimg.cn/f7acc92d089b4441853479ffdfb3de51.png)
![手机号判别是否合法](https://img-blog.csdnimg.cn/0a38361bf53c4bf38f9faaefc9706ee4.png)
![手机号判别是否合法](https://img-blog.csdnimg.cn/e02c64e34a674bfc97bede5074e73a65.png)
## 代码
### 导入 vant-weapp 组件：user-register.json

```json
{
  "usingComponents": {
  	"van-cell-group": "@vant/weapp/cell-group/index",
  	"van-field": "@vant/weapp/field/index",
  	"van-dropdown-menu": "@vant/weapp/dropdown-menu/index",
  	"van-dropdown-item": "@vant/weapp/dropdown-item/index",
  	"van-button": "@vant/weapp/button/index"
  }
}
```
### 编写布局文件：user-register.wxml

```html
<!-- pages/user-register/user-register.wxml -->
<view class="register-block">
  <view class="title">
    <text class="text">注册</text>
  </view>
  <van-cell-group class="input">
    <van-field label="学号" value="{{ studentNumber }}" placeholder="请输入学号" required clearable center bind:blur="setStudentNumber" />
    <van-field label="用户名" value="{{ userName }}" placeholder="请输入用户名" required clearable center bind:blur="setUsername" />
    <van-field label="班级" value="{{ className }}" placeholder="请输入所在班级" required clearable center bind:blur="setClassName" />
    <van-field label="手机号" value="{{ phoneNumber }}" placeholder="请输入手机号" error="{{ phoneLength || phoneFormat }}" error-message="{{ phoneError }}" required clearable center bind:blur="setphoneNumber" />
    <van-field label="性别" required use-input-slot>
      <view style="position: absolute; left: -16rpx;" slot="input">
        <van-dropdown-menu active-color="#92B6D5">
          <van-dropdown-item value="{{ gender }}" options="{{ option1 }}" bind:change="changeGender" />
        </van-dropdown-menu>
      </view>
    </van-field>
    <van-field label="校区" required use-input-slot>
      <view style="position: absolute; left: -16rpx;" slot="input">
        <van-dropdown-menu active-color="#92B6D5">
          <van-dropdown-item value="{{ area }}" options="{{ option2 }}" bind:change="changeArea" />
        </van-dropdown-menu>
      </view>
    </van-field>
    <van-field label="密码" value="{{ password }}" placeholder="请输入密码" required clearable center type="password" bind:blur="setPassword" />
    <van-field label="确认密码" value="{{ repassword }}" placeholder="请再次输入密码" error="{{ rePwdEqual }}" error-message="{{ errorMsg }}" required clearable center type="password" bind:blur="setRePassword" />
  </van-cell-group>
  <view class="login-block">
    <text class="text" bind:tap="gotoLogin">立即登录</text>
    <!-- <text class="">忘记密码</text> -->
  </view>
  <van-button class="btn" size="large" type="info" bind:tap="userRegister">注册</van-button>
</view>
```
### 编写样式文件：user-register.scss

```css
/* pages/user-register/user-register.scss */
.register-block{
  margin: 200rpx 20rpx 0 20rpx;

  .title{
    text-align: center;
    margin-bottom: 60rpx;

    .text{
      font-size: 60rpx;
      font-weight: 300;
    }
  }

  .login-block{
    text-align: right;
    margin: 10rpx 0;

    .text{
      color: gray;
      font-weight: 300;
      font-size: smaller;
    }
  }
}
```
### 判断手机号是否合法

```javascript
  /**
   * 输入手机号
   */
  setphoneNumber: function (event) {
    // console.log('username', event.detail.value)
    this.setData({
      phoneNumber: event.detail.value
    })
    const myReg = /^(((13[0-9{1})|(15[0-9]{1})|(18[0-9]{1})|(17[0-9]{1})) + \d{8})$/
    if (this.data.phoneNumber.length !== 0 && this.data.phoneNumber.length !== 11) {
      this.setData({
        phoneLength: true,
        phoneError: '手机长度有误'
      })
    } else if (this.data.phoneNumber.length !== 0 && !myReg.test(this.data.phoneNumber)) {
      this.setData({
        phoneFormat: true,
        phoneError: '手机号有误'
      })
    }
  },
```

### 完整js文件：user-register.js

```javascript
// pages/user-login/user-login.js

Page({
  /**
   * 页面的初始数据
   */
  data: {
    studentNumber: '',
    userName: '',
    className: '',
    phoneNumber: '',
    mygender: '',
    schoolarea: '',
    password: '',
    repassword: '',
    gender: 0,
    option1: [
      { text: '请选择性别', value: 0 },
      { text: '男', value: 1 },
      { text: '女', value: 2 }
    ],
    area: 0,
    option2: [
      { text: '请选择所在校区', value: 0 },
      { text: '北校区', value: 1 },
      { text: '南校区', value: 2 }
    ],
    // 错误提示
    rePwdEqual: false,
    phoneLength: false,
    phoneFormat: false
  },

  /**
   * 输入学号
   */
  setStudentNumber: function (event) {
    // console.log('username', event.detail.value)
    this.setData({
      studentNumber: event.detail.value
    })
  },

  /**
   * 输入用户名
   */
  setUsername: function (event) {
    // console.log('username', event.detail.value)
    this.setData({
      userName: event.detail.value
    })
  },

  /**
   * 输入所在班级
   */
  setClassName: function (event) {
    // console.log('username', event.detail.value)
    this.setData({
      className: event.detail.value
    })
  },

  /**
   * 输入手机号
   */
  setphoneNumber: function (event) {
    // console.log('username', event.detail.value)
    this.setData({
      phoneNumber: event.detail.value
    })
    const myReg = /^(((13[0-9{1})|(15[0-9]{1})|(18[0-9]{1})|(17[0-9]{1})) + \d{8})$/
    if (this.data.phoneNumber.length !== 0 && this.data.phoneNumber.length !== 11) {
      this.setData({
        phoneLength: true,
        phoneError: '手机长度有误'
      })
    } else if (this.data.phoneNumber.length !== 0 && !myReg.test(this.data.phoneNumber)) {
      this.setData({
        phoneFormat: true,
        phoneError: '手机号有误'
      })
    }
  },

  /**
   * 修改性别
   * @param {*} event
   */
  changeGender: function (event) {
    if (event.detail === 1) {
      this.setData({
        mygender: '男'
      })
    } else if (event.detail === 2) {
      this.setData({
        mygender: '女'
      })
    } else if (event.detail === 0) {
      wx.showToast({
        title: '请选择性别', // 提示的内容
        duration: 2000, // 延迟时间
        mask: true // 显示透明蒙层，防止触摸穿透
      })
    }
    console.log('改性别', event.detail + this.data.mygender)
  },

  /**
   * 修改所在校区
   */
  changeArea: function (event) {
    if (event.detail === 1) {
      this.setData({
        schoolarea: '北校区'
      })
    } else if (event.detail === 2) {
      this.setData({
        schoolarea: '南校区'
      })
    } else if (event.detail === 0) {
      wx.showToast({
        title: '请选择所在校区', // 提示的内容
        duration: 2000, // 延迟时间
        mask: true // 显示透明蒙层，防止触摸穿透
      })
    }
    console.log('改校区', event.detail + this.data.schoolarea)
  },

  /**
   * 输入密码
   */
  setPassword: function (event) {
    // console.log('password', event.detail.value)
    this.setData({
      password: event.detail.value
    })
  },

  /**
   * 再次输入密码
   */
  setRePassword: function (event) {
    // console.log('repassword', event.detail.value)
    this.setData({
      repassword: event.detail.value
    })
    if (this.data.password === this.data.repassword && this.data.password.length !== 0) {
      this.setData({
        rePwdEqual: false,
        errorMsg: ''
      })
    } else if (this.data.password !== this.data.repassword && this.data.password.length !== 0) {
      this.setData({
        rePwdEqual: true,
        errorMsg: '两次输入的密码不一致'
      })
    }
  },

  /**
   * 进入登录界面
   */
  gotoLogin: function () {
    // 当前要跳转到另一个界面，但是会保留现有界面
    wx.redirectTo({
      url: '../user-login/user-login'
    })
  },

  /**
   * 请求注册
   */
  userRegister: function () {
    // console.log('studentNumber', this.data.studentNumber)
    // console.log('userName', this.data.userName)
    // console.log('className', this.data.className)
    // console.log('phoneNumber', this.data.phoneNumber)
    // console.log('mygender', this.data.mygender)
    // console.log('schoolarea', this.data.schoolarea)
    const existStudentNumber = this.data.studentNumber.length !== 0
    const existUserName = this.data.userName.length !== 0
    const existClassName = this.data.className.length !== 0
    const existPhoneNumber = this.data.phoneNumber.length !== 0
    const existGender = this.data.mygender.length !== 0
    const existArea = this.data.schoolarea.length !== 0
    // console.log('studentNumber', existStudentNumber)
    // console.log('userName', existUserName)
    // console.log('className', existClassName)
    // console.log('phoneNumber', existPhoneNumber)
    // console.log('mygender', existGender)
    // console.log('schoolarea', existArea)
    if (existStudentNumber && existUserName && existClassName && existPhoneNumber && existGender && existArea && !this.data.rePwdEqual && !this.data.phoneLength && !this.data.phoneFormat) {
      if (this.data.password === this.data.repassword && this.data.password !== '') {
        // 发起网络请求
        wx.request({
          url: 'http://api/user/register',
          method: 'post',
          data: {
            student_number: this.data.studentNumber,
            class_name: this.data.className,
            name: this.data.userName,
            phone_number: this.data.phoneNumber,
            gender: this.data.mygender,
            area: this.data.schoolarea,
            password: this.data.password,
            second_password: this.data.repassword
          },
          header: {
            'content-type': 'application/x-www-form-urlencoded'
          },
          success(res) {
            console.log(res)
            if (res.data.code === 200) {
              wx.showToast({
                title: '注册成功！',
                icon: 'success'
              })
              wx.redirectTo({
                url: '/pages/user-login/user-login'
              })
            } else {
              wx.showToast({
                title: '注册失败！',
                icon: 'none'
              })
              console.log('注册失败！')
              console.log(res)
            }
          },
          fail(msg) {
            console.log(msg)
          }
        })
      }
    } else if (!existStudentNumber) {
      wx.showToast({
        title: '学号不能为空！',
        icon: 'none'
      })
    } else if (!existUserName) {
      wx.showToast({
        title: '用户名不能为空！',
        icon: 'none'
      })
    } else if (!existClassName) {
      wx.showToast({
        title: '班级不能为空！',
        icon: 'none'
      })
    } else if (!existPhoneNumber) {
      wx.showToast({
        title: '手机号不能为空！',
        icon: 'none'
      })
    } else if (!existGender) {
      wx.showToast({
        title: '请选择性别！',
        icon: 'none'
      })
    } else if (!existArea) {
      wx.showToast({
        title: '请选择所在校区！',
        icon: 'none'
      })
    } else {
      wx.showToast({
        title: '请按提示输入相关信息！',
        icon: 'none'
      })
    }
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
