---
title: 【微信小程序】字符超出一定长度变成省略号显示
date: 2021-08-24 14:44:32
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 效果
![](https://img-blog.csdnimg.cn/8f4603b9f5a543e0813df98542727928.png)

## 代码
```css
.item-content {
  width: 120rpx;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```
> 宽度需要设定；