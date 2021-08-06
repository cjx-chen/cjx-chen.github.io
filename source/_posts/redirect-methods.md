---
title: 微信小程序 页面跳转的四种方式
date: 2021-08-06 17:59:14
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## wx.navigateTo(OBJECT)
这是最普遍的一种跳转方式，其官方解释为：“保留当前页面，跳转到应用内的某个页面”类似于html中的 `window.location.href=" "`

```javascript
wx.navigateTo({
  url: 'test?id=1'
})
```
实际效果如下：
![](https://img-blog.csdnimg.cn/06cc6793b3a24847ab6bdc7ef151403d.png)
小程序中左上角有一个返回箭头，可返回上一个页面；

也可以通过方法  `wx.navigateBack` 返回原页面；

## wx.redirectTo(OBJECT)
关闭当前页面，跳转到应用内的某个页面。类似于html中的  `window.open('你所要跳转的页面');`

```javascript
wx.redirectTo({
  url: 'test?id=1'
})
```
效果如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/94f360118a68455dac2b725a28e12d3c.png)左上角没有返回箭头，不能返回上一个页面；

## wx.switchTab(OBJECT)
跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面；

app.json：

```json
{
  "tabBar": {
    "list": [{
      "pagePath": "index",
      "text": "首页"
    },{
      "pagePath": "other",
      "text": "其他"
    }]
  }
}
```

```javascript
wx.switchTab({
  url: '/index'
})
```
![](https://img-blog.csdnimg.cn/7f199fc9bff741c184aafea2819bf2ff.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
`wx.navigateTo` 和 `wx.redirectTo` 不允许跳转到 tabbar 页面，只能用 `wx.switchTab` 跳转到 tabbar 页面；

## wx.reLaunch(OBJECT)
关闭所有页面，打开到应用内的某个页面。

跟 `wx.redirectTo` 一样左上角不会出现返回箭头，但两者却不完全相同；

这里要提到小程序中的 `getCurrentPages()` 方法：

在 `wx.navigateTo` 中，每跳转一个新的页面，其原始页面就会被加入堆栈，通过调用 `wx.navigateBack(OBJECT)` 可通过获取堆栈中保存的页面返回上一级或多级页面；

`wx.redirectTo` 方法则不会被加入堆栈，但仍可通过 `wx.navigateBack(OBJECT)` 方法返回之前堆栈中的页面；

`wx.reLaunch` 方法则会清空当前的堆栈。

```javascript
// 此处是A页面
wx.navigateTo({
  url: 'B?id=1'
})

// 此处是B页面
wx.navigateTo({
  url: 'C?id=1'
})

// 在C页面内 navigateBack，将返回b页面
wx.navigateBack({
  delta: 1
})
```
```javascript
// 此处是B页面
wx.redirectTo({
 url: 'C?id=1'
})

// 在C页面内 navigateBack，则会返回a页面 
wx.navigateBack({
 delta: 1
})
```

```javascript
// 此处是B页面
wx.reLaunch({
 url: 'C?id=1'
})

// 在C页面内 navigateBack，则无效
```