---
title: 【HTML】点击直接下载文件
date: 2022-01-18 15:34:02
img: https://bkimg.cdn.bcebos.com/pic/fc1f4134970a304ed9002dcad3c8a786c9175ce4?x-bce-process=image/watermark,image_d2F0ZXIvYmFpa2UxMTY=,g_7,xp_5,yp_5/format,f_auto
categories: 
- 前端
tags:
- HTML
---

1、使用`<a>`标签

```html
<a href="/user/test/xxxx.txt" download="文件名.txt">点击下载</a>
```

这样当用户打开浏览器点击链接的时候就会直接下载文件。

但是有个情况，比如txt,png,jpg等这些浏览器支持直接打开的文件是不会执行下载任务的，而是会直接打开文件，这个时候就需要给a标签添加一个属性“download”;

实例如下：

移到标签`<a>`标签上可以显示文件路径，根据路径提示进行文件路径的补全

```html
<!DOCTYPE html> 
<html> 
    <head> 
        <metacharset="UTF-8"> 
        <title></title> 
    </head> 
    <body> 
        <a href="321.png" download="test.png">点击下载</a>   
    </body> 
</html>
```

若需从网页上传的图片中进行下载，可能会用到以下方法：

获取主机域名：`location.hostname`

获取端口号：`location.port`

2、使用按钮进行监听

按钮监听又可以分为两种方法，一是`window.open()`

```javascript
var $eleBtn1 = $("#btn1"); 
var $eleBtn2 = $("#btn2"); 

//已知一个下载文件的后端接口：https://codeload.github.com/douban/douban-client/legacy.zip/master 

//方法一：window.open() 
$eleBtn1.click(function(){ 
    window.open("https://codeload.github.com/douban/douban-client/legacy.zip/master"); 
});
```
二是表单提交

```javascript

//方法二：通过form 

$eleBtn2.click(function(){ 
    var$eleForm = $("<form method='get'></form>");
    $eleForm.attr("action","https://codeload.github.com/douban/douban-client/legacy.zip/master"); 
    $(document.body).append($eleForm); 

    //提交表单，实现下载 
    $eleForm.submit(); 
});
```