---
title: 【Html】解决 button 按钮点击后自动刷新页面的问题
date: 2022-01-09 10:45:44
img: https://bkimg.cdn.bcebos.com/pic/fc1f4134970a304ed9002dcad3c8a786c9175ce4?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2UxMTY=,g_7,xp_5,yp_5/format,f_auto
categories: 
- 前端
tags:
- Html
---

## 问题
页面上有一个查询按钮为 Button 标签，点击查询按钮后会自动刷新页面，令人费解，查资料后发现是 button 的默认行为导致的。

```html
<button class="btn btn-default active" id="btnAdd" click="selectData()">查询</button>
```
## 原因
button，input type=button 按钮在 IE 和 w3c，firefox 浏览器区别：
1、当在 IE 浏览器下面时，button 标签按钮，input 标签 type 属性为 button 的按钮是一样的功能，不会对表单进行任何操作。
2、但是在 W3C 浏览器，如Firefox下就需要注意了，button 标签按钮会提交表单，而input 标签 type 属性为 button 不会对表单进行任何操作。

## 解决办法
方法一：将 button 标签更换为 input

```html
<input class="btn btn-default active" id="btnAdd" value="查询" onclick="selectData()"></input>
```
方法二：为 button 按钮增加一个 type=”button” 属性

```html
<input type="button" class="btn btn-default active" id="btnAdd" value="查询" onclick="selectData()"></input>
```
