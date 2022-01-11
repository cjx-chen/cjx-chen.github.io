---
title: 【微信小程序】页面跳转传递参数（实体，对象）
date:    2022-01-11 15:32:43
img: https://static.sduan.com/web/upload/other/20211101/1635748984504710.jpeg
categories: 
- 微信小程序
- 需求
tags:
- 微信小程序
- JavaScript
---

## 场景
在一个列表中点击了某个 item，跳转到详情界面，那么我就需要把 item 的实体数据从列表页面传递到详情页面。

## 实现方法
那么我们来看看微信小程序给我们提供的API：
![](https://img-blog.csdnimg.cn/44e25d95721244eca25de811d25a720b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
这里大家可以清楚看到 api 中说到的如何传递参数，其实它这里指的参数仅仅是一些普通的数据类型，我们要传递的实体是 object 类型，那么我们需要先把实体转成 string 类型进行传递，在详情页面接受到在逆向转成实体，如下面这段示例：

```javascript
/**
 * 进入文章详情界面
 */
gotoArticleDetail: function (event) {
  // 拿到点击的index下标
  const index = event.currentTarget.dataset.index;
  // 将对象转为string
  const details = JSON.stringify(this.data.ArticleList[index]);
  // console.log('details', details);
  // 当前要跳转到另一个界面，但是会保留现有界面
  wx.navigateTo({
    url: `../article-detail/article-detail?details=${details}`
  });
},
```
这里我们用 `JSON.stringify()` 函数将实体转成 string 类型进行传递，那么我们在看看接收参数：

```javascript
/**
 * 生命周期函数--监听页面加载
 */
onLoad: function (options) {
  // console.log(options)
  const details = JSON.parse(options.details);
  console.log('details', details);
  this.setData({
    ArticleDetails: this.data.ArticleDetails.concat(details)
  });
  console.log('details', this.data.ArticleDetails);
},
```
这里我们在生命周期函数 onLoad 中获取我们传递的实体转的字符串，然后用 `JSON.parse()` 转成实体，最后赋值给我们的全局变量。

如果我们想要传递 Json 对象，也可以通过这样的方式进行传递。

## 遇到问题
小程序经常有跳转传参的功能，一般带一个 id 或者 name，title 之类很短的字段；但是如果带很多数据的话，很多人喜欢使用 json 转换，传参传一个对象过去，但这样仅限于很少的字段，不然就会出现报错：`SyntaxError: Unexpected end of JSON input`

## 产生原因
这是因为 navigateTo 方法携带的参数是有字符串长度限制的，超出部分就无法携带了，这就回导致传递过去的对象不闭合，使用 json 解析的时候就产生了报错。

## 解决方法
1、如果业务场景是从列表页面跳转到详情页面，那么推荐只携带少量字段,如 id，然后在详情页面使用 id 请求详情，这样就不用烦心字符长度超出的问题了（强烈推荐）。

2、如果不想请求新的数据，就用列表本身的字段，但是字符串超出的话，可以考虑下面方法。

> 使用 decodeURIComponent 和 encodeURIComponent 函数进行操作；

列表页面代码如下：

```javascript
/**
 * 进入文章详情界面
 */
gotoArticleDetail: function (event) {
  // 拿到点击的index下标
  const index = event.currentTarget.dataset.index;
  // 将对象转为string
  const details = encodeURIComponent(JSON.stringify(this.data.ArticleList[index]));
  // console.log('details', details);
  // 当前要跳转到另一个界面，但是会保留现有界面
  wx.navigateTo({
    url: `../article-detail/article-detail?details=${details}`
  });
},
```
详情页面代码：

```javascript
/**
 * 生命周期函数--监听页面加载
 */
onLoad: function (options) {
  // console.log(options)
  const details = JSON.parse(decodeURIComponent(options.details));
  console.log('details', details);
  this.setData({
    ArticleDetails: this.data.ArticleDetails.concat(details)
  });
  console.log('details', this.data.ArticleDetails);
},
```
`encodeURIComponent()` 函数可把字符串作为 URI 组件进行编码。 需要编码传送，解码接收，这样就可以解决字符串长度的问题。