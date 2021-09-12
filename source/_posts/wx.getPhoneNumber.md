---
title: 【微信小程序】获取手机号
date: 2021-09-12 20:33:58
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
- API
---

## 场景
在小程序开发中，获取用户信息、获取手机号是最常用到的功能。

官方文档说明如下：
[https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/getPhoneNumber.html](https://developers.weixin.qq.com/miniprogram/dev/framework/open-ability/getPhoneNumber.html)

## 效果
![](https://img-blog.csdnimg.cn/064e0a5e85ac41098a75547c3b5e52d5.gif)
## 代码
### demo.json：初始化json文件
```json
{
  "usingComponents": {}
}
```

### demo.wxml：初始化布局文件
```html
<button type="warn" open-type="getPhoneNumber" bindgetphonenumber="getPhoneNumber"> getPhoneNumber </button>
```

### demo.js：封装获取手机号方法
```javascript
  /**
   * 获取手机号
   * @param {*} e
   */
  getPhoneNumber(e) {
    console.log('getPhoneNumber:' + e.detail);
    console.log(e.detail.errMsg, 'err');
    console.log(e.detail.iv, 'iv');
    console.log(e.detail.encryptedData, 'encryptedData');
    const ivRes = e.detail.iv;
    const encryptedDataRes = e.detail.encryptedData;
    if (e.detail.errMsg === 'getPhoneNumber:ok') {
      wx.login({
        success (res) {
          if (res.code) {
            console.log('encryptedData', encryptedDataRes);
            console.log('iv', ivRes);
            wx.request({
              url: 'https://api/user/phoneNumber',
              data: {
                code: res.code,
                encryptedData: encryptedDataRes,
                iv: ivRes
              },
              method: 'post',
              header: {
                'content-type': 'application/json' // 默认值
              },
              success: function (res) {
                console.log(res);
              }
            });
          }
        },
        fail (msg) {
          console.log(msg);
        },
        complete: () => {}
      });
    }
  },
```
