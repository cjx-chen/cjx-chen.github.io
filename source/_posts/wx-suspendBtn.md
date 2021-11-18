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

需要制作一个如下图右下角的悬浮按钮：
![](https://img-blog.csdnimg.cn/52f6d623a1d74d6ca437ddce08e2fcc4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_11,color_FFFFFF,t_70,g_se,x_16)

## 代码

### index.wxml

```html
<!-- 发布悬浮按钮 -->
<view class="releaseBtn" bind:tap="gotoRelease">
  <image class="releaseIcon" src="/images/pen.png" />
</view>
```

### index.scss

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