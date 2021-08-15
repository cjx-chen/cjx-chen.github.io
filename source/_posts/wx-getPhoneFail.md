---
title: 【微信小程序】手机号码解析失败解决方法
date:  2021-08-15 20:05:23
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
- API
---

## 场景
在小程序开发中，获取用户信息、获取手机号是最常用到的功能。

但是有时可能会遇到“手机号解析失败”的问题，这个时候我们检查下代码是否是在获取手机号的回调中才调用的 `wx.login` 的方法。

官方文档说明如下：
[https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/getPhoneNumber.html#%E4%BB%A3%E7%A0%81%E7%A4%BA%E4%BE%8B](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/getPhoneNumber.html#%E4%BB%A3%E7%A0%81%E7%A4%BA%E4%BE%8B)
![](https://img-blog.csdnimg.cn/230cf3031fea423ca3bd1ebe68688ff2.png)
## 解决方法
所有解决办法是提前调 `wx.login`，在获取手机号的回调方法中取检验登录状态，代码如下：

```javascript
onLoad: function (options) {
    wx.login({
      success: res => {
        that.setData({
          code: res.code
        })
      }
    })//先登录在获取手机号
  },
  getPhoneNumber(e) {
    let encryptedData = e.detail.encryptedData
    let iv = e.detail.iv
    wx.checkSession({
      success() {
        //session_key 未过期，并且在本生命周期一直有效
      },
      fail() {
        // session_key 已经失效，需要重新执行登录流程
        wx.login({
          success: res => {
            code = res.code
            that.setData({
              code: code
            })
          }
        })
      },
      complete() {
        //将code,encryptedData,iv传给后台进行解密
      }
    })
  }
```