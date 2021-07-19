---
title: 组件库 Vant weapp 的使用
date: 2020-08-12 19:30:10
img: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg-blog.csdnimg.cn%2Fimg_convert%2Fde2eb89454a66222dcaf49f5848167d5.png&refer=http%3A%2F%2Fimg-blog.csdnimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1629297773&t=7c0e483460feced14a83396640fa2cfd
categories: 
- 安装配置教程
- 微信小程序
tags:
- 微信小程序
---

## 项目初始化
###  第一步
新建一个云开发的小程序项目：
![](https://img-blog.csdnimg.cn/20200811140904962.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
把不需要的东西都删掉：
![](https://img-blog.csdnimg.cn/20200811141121466.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
将 index.wxss 、index.wxml 、index.js 、app.wxss 清空，初始化 index.js：

```javascript
Page({

  /**
   * 页面的初始数据
   */
  data: {
    
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    
  },

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady: function () {
    
  },

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {
    
  },

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {
    
  },

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload: function () {
    
  },

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh: function () {
    
  },

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom: function () {
    
  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage: function () {
    
  }
})
```
将 app.json 改成这样：

```json
{
  "pages": [
    "pages/index/index"
  ],
  "window": {
    "backgroundColor": "#F6F6F6",
    "backgroundTextStyle": "light",
    "navigationBarBackgroundColor": "#F6F6F6",
    "navigationBarTitleText": "云开发 QuickStart",
    "navigationBarTextStyle": "black"
  },
  "sitemapLocation": "sitemap.json",
  "style": "v2"
}
```
###  第二步
打开官网 [https://vant-contrib.gitee.io/vant-weapp/#/intro](https://vant-contrib.gitee.io/vant-weapp/#/intro)：
![](https://img-blog.csdnimg.cn/20200811141800645.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
点击快速上手，按照其中的步骤进行操作：
![](https://img-blog.csdnimg.cn/20200811142053123.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
打开电脑命令行，确保自己电脑安装过 Node.js ：
![](https://img-blog.csdnimg.cn/20200811142125280.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
然后右击项目文件夹，点击【在终端中打开】：
![](https://img-blog.csdnimg.cn/20200811142239339.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
先输入：
![](https://img-blog.csdnimg.cn/20200811142940185.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
再输入：
![](https://img-blog.csdnimg.cn/20200811143000819.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
点击右上角【详情】-> 【本地设置】-> 勾选【使用 npm 模块】：
![](https://img-blog.csdnimg.cn/20200811143144157.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
最后点击【工具】->【构建 npm】：
![](https://img-blog.csdnimg.cn/20200812183159749.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
弹出下图这个框即证明该项目建立完毕：
![](https://img-blog.csdnimg.cn/20200812183237484.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
## 组件的使用
文档中的写的很详细，只要看文档基本上都能完成， 我们来示例一下复杂类型的组件使用：

以**下拉菜单**为例：

将 app.json 修改：
![](https://img-blog.csdnimg.cn/20200812191811410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
写好 index.wxml：
![](https://img-blog.csdnimg.cn/20200812191855146.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
在 index.js 中写好事件绑定：

```javascript
Page({

  /**
   * 页面的初始数据
   */
  data: {
    show: false,
    actions: [
      {
        name: '选项1',
      },
      {
        name: '选项2',
      },
      {
        name: '选项3',
        subname: '副文本',
        openType: 'share',
      },
    ],
    value:""
  },

  onTap() {
    this.setData ({
      show: true
    })
  },

  onClose() {
    this.setData ({
      show: false
    })
  },

  onSelect(res) {
    this.setData ({
      value: res.detail.name
    })
    
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    
  },

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady: function () {
    
  },

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {
    
  },

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {
    
  },

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload: function () {
    
  },

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh: function () {
    
  },

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom: function () {
    
  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage: function () {
    
  }
})
```

运行结果如下：
![](https://img-blog.csdnimg.cn/2020081219284788.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
基本操作就是这样啦，掰掰


