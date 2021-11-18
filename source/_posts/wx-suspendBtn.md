---
title: 【微信小程序】悬浮按钮
date:  2021-11-18 11:00:39
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 效果
需要制作一个底部居右的悬浮按钮：
![](https://img-blog.csdnimg.cn/1037e3b4271844f5b29e2843890774ae.png)

需要制作一个固定在底部居中的悬浮按钮：
![](https://img-blog.csdnimg.cn/5b51f40116cf4db0999ab7b5813ddf4c.png)

## 代码
### 底部居右
#### index.wxml
```html
<!-- 发布悬浮按钮 -->
<view class="releaseBtn" bind:tap="gotoRelease">
  <image class="releaseIcon" src="/images/pen.png" />
</view>
```
#### index.scss

```css
// 发布悬浮按钮
.releaseBtn {
  position: fixed;
  bottom: 50px;
  right: 50px;

  .releaseIcon {
    width: 80rpx;
    height: 80rpx;
    border-radius: 50%;
    border: solid 1rpx #FFC64B;
    padding: 20rpx;
  }
}
```
### 底部居中
#### index.wxml
```html
<view class="btnRelease">
  <van-button class="release" round type="info" disabled="{{disabled}}" color="#FFC64B">
    发布
  </van-button>
</view>
```
#### index.scss

```css
  .btnRelease{
    position: fixed;
    bottom: 120rpx;
    display: flex;
    width: 100%;
    justify-content: center;
    text-align: center;

    button {
      width: 220rpx;
      height: 58rpx;
    }
  }
```
