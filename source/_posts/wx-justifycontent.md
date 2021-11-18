---
title: 【微信小程序】div 标签内实现垂直居中
date:  2021-11-02 22:18:00
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
- 需求
tags:
- 微信小程序
- CSS
---

## 效果

![之前效果](https://img-blog.csdnimg.cn/c8f64e6d15014f679e6f210e99792575.png)
![目标效果](https://img-blog.csdnimg.cn/83c02789b6e54e00acd12b41207b0909.png)

## 代码

### index.wxml

```html
 <van-button class="btn" size="large" type="primary" bind:tap="getUserInfo">
   <div style="display: flex; flex-direction: row; justify-content: space-around;">
     <image src="../../images/wechat.png" style="width: 40rpx; height: 40rpx; margin-right: 10rpx;" />
     <p>微信授权登录</p>
   </div>
 </van-button>
```