---
title: 【微信小程序】报错解决方法 [TypeError:N.length is not a function]
date:  2021-09-12 10:54:13
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
- 报错解决方法
---

## 解决方法

`N.length()` 后面的括号去掉；

## 原因分析

`N.length` 是属性不是方法，不能在后面加括号执行；

