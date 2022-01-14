---
title: 【JavaScript】实现延时3秒刷新
date: 2022-01-14 16:11:48
img: https://pic1.zhimg.com/v2-bde07fdceb700b45ea02f16e3bb099e7_1440w.jpg?source=172ae18b
categories: 
- 前端
tags:
- JavaScript
---

## 代码
```javascript
setTimeout(function (){
	window.location.reload();
}, 3000);
```
