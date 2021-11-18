---
title: 【微信小程序】给后台返回的对象数组每个对象添加指定新属性
date: 2021-11-01 16:17:32
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 微信小程序
tags:
- 微信小程序
- JavaScript
---
## 效果

后台返回数据：
![](https://img-blog.csdnimg.cn/4e4cd52fa40041d89b47e75c40070331.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
添加属性后数据：
![](https://img-blog.csdnimg.cn/cf10da502cca4975b3bbe7d2d68ce101.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

## 说明

`auto` 与 `seeMore` 属性是在请求到后台的数据后逐条添加的；

## 代码

主要补充的是页面加载时 js 中的初始化数据方法部分：

```javascript
Component({
  /**
   * 组件的属性列表
   */
  properties: {
    // 定义一个list数组对象接收父组件传的数据
    list: {
      type: Array,
      value: []
    },
    scene: {
      type: String,
      value: ''
    }
  },

  /**
   * 组件的初始数据
   */
  data: {

  },

  /**
   * 组件的方法列表
   */
  methods: {
    /**
     * 添加展开/收起属性
     */
    init: function () {
      const that = this;
      // 给后台返还的数据就对象加对象属性值
      that.properties.list.forEach((r) => { // list是后台返回的数据
        r.auto = false; // r = list[0]的所有数据，这样直接 r.新属性 = 属性值 即可
        r.seeMore = false;
      });
      that.setData({ // 这里划重点 需要重新setData 下才能js 和 wxml 同步，wxml才能渲染新数据
        list: that.properties.list
      });
      console.log('list', that.properties.list);
    }
  },

  /**
   * 组件的生命周期
   */
  lifetimes: {
    attached: function () {
      // 在组件实例进入页面节点树时执行

    },
    detached: function () {
      // 在组件实例被从页面节点树移除时执行

    },
    ready: function () {
      const that = this;
      that.init();
    }
  }
});
```

如果不是写在组件上的，则：

```javascript
/**
 * 添加展开/收起属性
 */
init: function () {
  const that = this;
  // 给后台返还的数据就对象加对象属性值
  that.data.list.forEach((r) => { // list是后台返回的数据
    r.auto = false; // r = list[0]的所有数据，这样直接 r.新属性 = 属性值 即可
    r.seeMore = false;
  });
  that.setData({ // 这里划重点 需要重新setData 下才能js 和 wxml 同步，wxml才能渲染新数据
    list: that.data.list
  });
  console.log('list', that.data.list);
}
```

别忘了在生命周期函数 `onLoad`，加载此方法；