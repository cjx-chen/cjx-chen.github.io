---
title: 【jQuery】跳转另一个页面
date: 2022-01-09 11:21:21
img: https://img.php.cn/upload/article/000/000/194/ffb4ed33d825a51cd2aa47468fe5219c.png
categories: 
- 前端
tags:
- Jquery
---

1.我们可以利用http的重定向来跳转

```javascript
window.location.replace("http://www.baidu.com");
```

2.使用 href 来跳转

```javascript
window.location.href = "http://www.baidu.com";
```

3.使用 jQuery 的属性替换方法

```javascript
// 3.1 
$(location).attr('href', 'http://www.baidu.com');

// 3.2 
$(window).attr('location','http://www.baidu.com');

// 3.3 
$(location).prop('href', 'http://www.baidu.com')
```
