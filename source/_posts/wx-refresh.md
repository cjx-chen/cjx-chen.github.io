---
title: 【微信小程序】在组件中刷新页面
date:   2021-11-06 20:25:10
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 代码

在组件页面的 js 对应的函数中加入：

```javascript
const page = getCurrentPages().pop(); //当前页面
if (page == undefined || page == null) return; 
page.onLoad(); //或者其它操作
```

