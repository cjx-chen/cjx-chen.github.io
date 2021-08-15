---
title: 【微信小程序】用户授权以及判断登录是否过期的方法
date:  2021-08-15 19:50:03
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
- API
---

## 实现效果
![](https://img-blog.csdnimg.cn/7399351a205e4aa7b2e75a7163760977.png)

## 场景
在打开小程序时判断用户是否过期(如果未过期则重新登录)，然后获取用户信息，进而在前台显示；

主要实现两个功能：

1. 判断登录是否过期，如果过期则就重新登录，如果没过期就提示未过期；

2. 获取用户的信息，并在前台显示；

## 代码
要实现在打开小程序时判断用户是否过期，则需要把代码写到 app.js 里：

```javascript
// app.js

App({
  async onLaunch() {
    // 验证登录是否过期
    wx.checkSession({
      success: function (res) {
        console.log(res, '登录未过期');
        wx.showToast({
          title: '登录未过期'
        });
      },
      fail: function (res) {
        console.log(res, '登录已过期');
        wx.showModal({
          title: '提示',
          content: '登录已过期，请重新登录',
          success(res) {
            if (res.confirm) {
              // 调用接口获取登录凭证（code）
              wx.login({
                success(res) {
                  console.log(res);
                  if (res.code) {
                    // 发起网络请求
                    wx.request({
                      url: '<登录接口>',
                      method: 'post',
                      data: {
                        code: res.code
                      },
                      header: {
                        'content-type': 'application/x-www-form-urlencoded'
                      },
                      success(res) {
                        console.log(res);
                        if (res.data.code === 1) {
                          wx.switchTab({
                            url: '<首页url>'
                          });
                        } else {
                          console.log('登录失败！');
                          console.log(res);
                        }
                      },
                      fail(msg) {
                        console.log(msg);
                      }
                    });
                  } else {
                    console.log('登录失败！' + res.errMsg);
                  }
                }
              });
              wx.getSetting({
                success(res) {
                  if (res.authSetting['scope.userInfo']) {
                    // 已经授权，可以直接调用 getUserInfo 获取头像昵称
                    wx.getUserInfo({
                      success: function (res) {
                        console.log(res.userInfo);
                      }
                    });
                  } else {
                    wx.navigateTo({
                      url: '<注册url>'
                    });
                  }
                }
              });
            } else if (res.cancel) {
              wx.switchTab({
                url: '<首页url>'
              });
            }
          }
        });
      }
    });
  }
});
```
