---
title: 【微信小程序】用 setData 方法修改 data 中对象数组某一项的属性值
date:   2021-11-07 16:28:44
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
---

## 方法

1. 先用一个变量表示对象的属性值（字符串）或数组的某一项的值（字符串拼接起来）；
2. 将变量写在`[]`里面即可修改；

## 代码

### index.js

```javascript
Page({
  data: {
    // 普通：
    text1:1,
    // 对象的属性值：
    text2:{
      text2_1:2,
    },
    // 数组：
    text3:[3,3,3],
    // 数组和对象结合：
    text4:[
      {
        bool:false,
        num:4
      },
      {
        bool:true,
        num:44
      }
    ]
  },
  text1:function(){
    this.setData({
      text1:11111,
    });
  },
  text2: function () {
    var t2 = "text2.text2_1";
    this.setData({
      [t2]: 22222,
    });
  },
  text3: function () {
    var t3 = "text3["+0+"]";
    this.setData({
      [t3]: 33333,
    });
  },
  text4: function () {
    var t4 = "text4["+0+"].num";
    this.setData({
      [t4]: 44444,
    });
  }
})
```

### index.wxml

```html
<view class="page">
  <view catchtap="text1">{{text1}}</view>
  <view catchtap="text2">{{text2.text2_1}}</view>
  <view catchtap="text3">{{text3[0]}}</view>
  <view catchtap="text4">{{text4[0].num}}</view>
</view>
```

## 效果

![](https://img-blog.csdnimg.cn/c0132a54a21f4b4eba4c9790071b66b4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_10,color_FFFFFF,t_70,g_se,x_16)