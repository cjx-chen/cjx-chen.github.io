---
title: 【微信小程序】wx.login 和 wx.getUserProfile 同时使用问题
date:  2021-08-14 18:17:44
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
- API
---

## 场景
在使用微信登录时，通常会在调用 `wx.login` 获取 `code` 后再通过 `wx.getUserProfile` 获取 `iv` 和 `encryptedData` （加密数据）一起发到后端进行登录验证；

但是，在实际使用中如果在 `wx.login` 方法调用后再调用 `wx.getUserProfile` 会报错；

## 官方解释
![](https://img-blog.csdnimg.cn/ede8acb9f67646459cccccf61c046ade.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
也就是说，不能在调用方法的回调中使用 `wx.getUserProfule()`；

## 解决方法
**使用Promise.all()方法实现平级调用；**

> `Promise.all()` 方法接收一个 `promise` 的 `iterable` 类型（注：`Array`，`Map`，`Set` 都属于ES6 的 `iterable` 类型）的输入，并且只返回一个 `Promise` 实例， 那个输入的所有`promise` 的 `resolve` 回调的结果是一个数组。这个 `Promise` 的 `resolve` 回调执行是在所有输入的 `promise` 的 `resolve` 回调都结束，或者输入的 `iterable` 里没有 `promise` 了的时候。它的 `reject` 回调执行是，只要任何一个输入的 `promise` 的 `reject` 回调执行或者输入不合法的 `promise` 就会立即抛出错误，并且 `reject` 的是第一个抛出的错误信息。

简单点说就是会等到两个方法都回调成功该方法才会返回来值，返回值是一个数组。

## 代码
### 封装 `wx.login` 和 `wx.getUserProfile` 两个接口：

```javascript
/**
 * 使用promise封装用户信息接口
 */
getUserInfo:function(){
  return new Promise((resolve,reject) => {
    wx.getUserProfile({
      desc: '用户登录', // 声明获取用户个人信息后的用途，后续会展示在弹窗中，请谨慎填写
      success: (res) => {
        resolve(res)
      },
      fail:(err) => {
        reject(err)
      }
    })
  })
},

/**
 * 使用promise封装wx.login接口
 */
getLogin:function(){
 return new Promise((resolve,reject) => {
   wx.login({
     success (res) {
       resolve(res)
    },
    fail: (err) => {
      reject(err)
   	}
  })
 })
},
```

### 封装登录接口

```javascript
/**
 * 登录接口
 */
login: function(){
  let userRes = this.getUserInfo()
  let loginRes = this.getLogin()
  //使用promise.all()平级调用
  Promise.all([userRes,loginRes]).then((res) => {
   console.log(res)
   let param = {
     code: res[1].code,
     iv: res[0].iv,
     encryptedData: res[0].encryptedData
   }
   let data = {
     method: "post",
     url: api.apiName.wxLogin,
     params: param
   }
   request.request(data).then(res => {
     wx.setStorageSync('token', res.data)
     wx.setStorageSync('hasLogin', true)
     //获取用户信息
     let data = {
       method: "get",
       url: api.apiName.getUserInfo,
       params: null
     }
     request.request(data).then(res2 => {
       wx.hideLoading({})
       wx.setStorageSync('userInfo', res2.data)
     }).catch(err => {
       wx.hideLoading({})
       console.log(err.msg)
     })
     setTimeout(function(){
       wx.switchTab({
          url: '../../index/index',
       })
     },1500)
    }).catch(err => {
      console.log(err.msg)
    })
  })
}
```
