---
title: 【Vue3】跨域问题 [The value of the 'Access-Control-Allow-Origin' header in the response must not be the..]
date:  2022-01-14 18:34:57
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- Vue3
tags:
- Vue3
- Javascript
- 报错解决方法
---

## 场景
vue 项目中 axios 请求数据的时候请求失败，出现跨域问题。

## 报错信息

`
The value of the 'Access-Control-Allow-Origin' header in the response must not be the wildcard
`

## 解决方法
**withCredentials 属性**

CORS 请求默认不发送 Cookie 和 HTTP 认证信息。如果要把 Cookie 发到服务器，一方面要服务器同意，指定 `Access-Control-Allow-Credentials` 字段。

出现这个报错信息很可能是你在前端设置了 `withCredentials = true;` 你可以去掉这个设置。