---
title: 【微信小程序】全局变量的定义与使用
date:   2021-08-31 11:18:39
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 全局变量的定义

在你初次打开 app.js 文件时，很容易混淆。在 `onLaunch` 函数里是有个 `globalData` 对象，但请注意，你的全局变量不是写在这里，而是另外在函数外定义一个 `globalData`。

例如下图：
![](https://img-blog.csdnimg.cn/e74993b3afd946acb2f01bfccca31dfa.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Za15Za15Za15Za16KaB5oqx5oqx,size_20,color_FFFFFF,t_70,g_se,x_16)
`globalData` 一定要定义在与函数同级的位置。然后在`globalData` 里面编写你的全局变量的值。

## 全局变量的赋值

一般初始化的时候会给空值或者固定值，然后通过后期的小程序使用过程中改变全局变量。

全局变量值得改变有两个地方。一是在 app.js 文件中改变。二是在其他 js 文件中改变。

在 app.js 中，你只需要通过 `this.globalData.XXXX = XXX` 进行赋值即可。不能使用 `this.setData` 进行赋值。

在其他 js 文件中，我们首先要引入全局变量：

```javascript
const app = getApp()
```

然后通过 `app` 去调用 `globalData`。

例如：

```javascript
app.globalData.XXXX = XXX
```

## 全局变量的使用

使用全局变量分为两种情况，一是在 app.js 文件中使用，二是在其他 js 文件中使用。

在 app.js 文件中使用时直接通过 `this.globalData.XXXX` 即可使用。

在其他 js 文件中使用先获取全局对象：

```javascript
const app = getApp()
```

接着通过 `app.globalData.XXXX` 调用即可。

## 全局变量的有效期

全局变量的有效期只存在于当前使用的状态下，一旦小程序被用户退出或者微信自身清理之后，将不保留全局变量。所以你需要根据自己的需求进行设置全局变量，合理的应用。