---
title: 【jQuery】获取url参数及url加参数的方法
date: 2022-01-09 10:31:27
img: https://img.php.cn/upload/article/000/000/194/ffb4ed33d825a51cd2aa47468fe5219c.png
categories: 
- 前端
tags:
- Jquery
---

1、jquery 获取 url 很简单，代码如下：
```javascript
window.location.href;
```
其实只是用到了 javascript 的基础的 window 对象，并没有用 jquery 的知识。

2、jquery 获取 url 参数比较复杂，要用到正则表达式，所以学好 javascript 正则式多么重要的事情

首先看看单纯的通过 javascript 是如何来获取 url 中的某个参数：

```javascript
//获取url中的参数
function getUrlParam(name) {
 var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)"); //构造一个含有目标参数的正则表达式对象
 var r = window.location.search.substr(1).match(reg); //匹配目标参数
 if (r != null) return unescape(r[2]); return null; //返回参数值
}
```
通过这个函数传递 url 中的参数名就可以获取到参数的值，比如 url 为

http://localhost:8080/works?worksid=1

我们要获取 worksid 的值，可以这样写：
```javascript
var worksid = getUrlParam('worksid');
```
明白了 javascript 获取 url 参数的方法，我们可以通过这个方法为 jquery 扩展一个方法来通过 jquery 获取 url 参数，下面的代码为 jquery 扩展了一个 `getUrlParam()` 方法

```javascript
(function ($) {
  $.getUrlParam = function (name) {
   var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
   var r = window.location.search.substr(1).match(reg);
   if (r != null) return unescape(r[2]); return null;
  }
 })(jQuery);
```
为 jquery 扩展了这个方法了之后我们就可以通过如下方法来获取某个参数的值了：

```javascript
var worksid = $.getUrlParam('worksid');
```

> 用上面的方法获取 url 中的参数时，url 中传递的中文参数在解析的时候无论怎么测试，获取的都是乱码。原因是在传递参数时，对汉字编码使用的是 encodeURI ，而上面的方法在解析参数编码时使用的是 unescape，修改为 decodeURI 就可以了。
> 综上： javascript对参数编码解码方法要一致：
escape()   unescape()
encodeURI()   decodeURI()
encodeURIComponent()    decodeURIComponent() 
