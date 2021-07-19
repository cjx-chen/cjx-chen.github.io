---
title: 微信小程序入门基础与实践
date: 2020-05-30 14:07:48
img: https://ss2.meipian.me/users/9402500/origincd3ac259910cbb278b3d8aae6a1bbea4.jpg?imageView2/2/w/750/h/1400/q/80
categories: 
- 安装配置步骤
- 微信小程序
tags:
- 微信小程序
---

## 小程序开发工具与基础
**小程序开发准备：**

 1. 申请小程序账号（ appid ）
 2. 下载并安装微信开发者工具

具体步骤如下：

 - 先进入 [微信公众平台](https://mp.weixin.qq.com/) ，下拉页面，把鼠标悬浮在小程序图标上
 ![](https://img-blog.csdnimg.cn/2020053011533742.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
 - 然后点击 [小程序开发文档](https://developers.weixin.qq.com/miniprogram/dev/framework/) 
 ![](https://img-blog.csdnimg.cn/20200530115427561.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
 - 照着里面给的步骤，就可以申请到小程序账号了。
 - 然后就可以下载 [开发者工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html) 了
 - 下载完打开后的界面就是这个样子
![](https://img-blog.csdnimg.cn/20200530121537636.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
下面让我们来新建一个小程序开发项目：
![](https://img-blog.csdnimg.cn/20200530141309224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

在AppID输入自己刚刚注册的AppID就可以，或者使用测试号，创建后的页面是这样的：
![](https://img-blog.csdnimg.cn/20200530130222155.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

## 编写第一个小程序页面
包括的知识点有：
 - 小程序文件类型与目录结构
 - 注册小程序页面，View、Image、Text 等组件的基本用法
 - Flex 弹性盒子模型
 - 移动端分辨率及小程序自适应单位 RPX
 
 
先把多余的东西删掉
![](https://img-blog.csdnimg.cn/20200530130429651.png)
再重新新建 app.js 、app.json、app.wxss 文件
![](https://img-blog.csdnimg.cn/20200530130540918.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
再在 pages 文件里新建一个 welcome 目录，把文件建全
![](https://img-blog.csdnimg.cn/20200530130757627.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
打开 [微信开放文档](https://developers.weixin.qq.com/miniprogram/dev/reference/configuration/app.html) ，点击框架，查看小程序的配置
![](https://img-blog.csdnimg.cn/20200530131445860.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
将红框的代码复制到 app.json 中，再针对自己创建的目录进行修改：

```json
{
	"pages": ["pages/welcome/welcome"]
}
```

打开 welcome.json，因为 json 文件不能为空，所以加上一个花括号，或者可以删除 json 文件：

```json
{

}
```

再打开 welcome.js 文件，加入以下代码：

```javascript
Page({

})
```

最后在 welcome.wxml 文件中加入以下代码：

```html
<view>
	<text>hello</text>
</view>
```

就会出现这个界面啦：
![](https://img-blog.csdnimg.cn/20200530132257442.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
在根目录下新建一个 images 文件夹，存放图片，然后调用图片；
再在 welcome.wxml 上加入以下代码：

```html
<!-- wxml 是用来编写页面骨架的文件 -->
<!-- 在小程序中 view 的功能基本上是等同于 div 的，主要功能有容器、分隔文档 -->
<view>
  <image style="width:200rpx; height:200rpx;" src="/images/image.png"></image>
  <text>Hello, Jessie</text>
  <!-- <button></button> -->
  <view>
    <text>开启小程序之旅</text>
  </view>
</view>
```
下面我们尝试将样式的代码都转移到 welcome.wxss 文件中：

```css
.container{
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #b3d4db;
}

page{
  background-color: #b3d4db;
  height: 100%;
}

.user-image{
  width: 200rpx;
  height: 200rpx;
  margin-top: 160rpx;
  border-radius: 50%;
}

.user-name{
  margin-top: 60rpx;
  font-size: 32rpx;
  font-weight: bold;
}

.moto{
  font-size: 22rpx;
  font-weight: bold;
  line-height: 80rpx;
  color: #405f80;
}

.moto-container{
  border: 1px solid #405f80;
  height: 80rpx;
  width: 200rpx;
  border-radius: 5px;
  text-align: center;
  margin-top: 200rpx;
}

/* flex 布局 弹性盒子模型 */
```
再补充一下 app.wxss 文件内的代码：

```css
text{
  font-family: MicroSoft Yahei;
}
```
再打开 app.json 更改一下顶部状态栏的颜色：

```json
{
  "pages": ["pages/welcome/welcome"],
  "window": {
    "navigationBarBackgroundColor": "#b3d4db"
  }
}
```
下面是 welcome.wxml 的代码：

```html
<!-- wxml 是用来编写页面骨架的文件 -->
<!-- 在小程序中 view 的功能基本上是等同于 div 的，主要功能有容器、分隔文档 -->
<view class="container">
  <image class="user-image" src="/images/mayor.jpg"></image>
  <text class="user-name">Hello, Jessie</text>
  <!-- <button></button> -->
  <view class="moto-container">
    <text class="moto">开启小程序之旅</text>
  </view>
</view>
```
我们的第一个小程序页面就做好啦：
![](https://img-blog.csdnimg.cn/20200530140656576.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
