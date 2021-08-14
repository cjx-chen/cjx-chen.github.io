---
title: 【微信小程序报错解决方法】TypeError: Cannot read property ‘setData‘ of undefined
date:  2021-08-14 17:51:39
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
- 报错解决方法
---

## 场景
自己在调用 `wx.getSystemInfo({})` 时，开发工具自动补全了代码。在 `success` 回调中按照以往的写法调用 `this.setData({ });` 时，报错：`TypeError: Cannot read property 'setData' of undefined`。

相关代码如下：

```javascript
  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    wx.getSystemInfo({
      success: function (res) {
        console.log(res);
        this.setData({
          system_info: res.brand,
        });
      },
      fail: function (res) {
        this.myShowError("获取手机系统信息")
      },
      complete: function (res) { },
    })

  },
```
仔细对比和之前绑定事件调用 `this.setData({ });` ，调用方式并没有什么差别。查阅资料发现要改成 `success: (res) => {};` 这种写法，而不是 `success: function (res) {};`，就可以正常使用了。

```javascript
  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    wx.getSystemInfo({
      success: (res) => {
        console.log(res);
        this.setData({
          system_info: res.brand,
        });
      },
      fail: function (res) {
        this.myShowError("获取手机系统信息")
      },
      complete: function (res) { },
    })

  },
```

## 解决方法
将下列代码：

```javascript
success: function (res) {
   this.setData({})
}
```
改成以下代码：

```javascript
success: (res) =>  {
   this.setData({})
}
```

## 原因分析
原因：两种写法 `this` 指向不同；

将下列两种情况分别运行一遍：
```javascript
success: (res) => {
   console.log("(res) => { }时：" + this);
},
```
```javascript
success: function (res){
   console.log("function (res)时：" + this);
},
```
运行结果对比分析：

```powershell
function (res)时：undefined
(res) => { }时：[object Object]
```
`function (res)` 写法时 ，`this` 是 `undefined` 未定义的。
`(res) => { }` 写法时 `this` 是 `Object`。

## 分析总结
1. 如果函数作为对象的方法调用，`this` 指向的是这个上级对象，即调用方法的对象。
2. 如果是构造函数中的 `this`，则 `this` 指向新创建的对象本身。