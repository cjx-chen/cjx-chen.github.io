---
title: 【JavaScript】封装Toast弹窗
date: 2022-01-09 11:25:39
img: https://pic1.zhimg.com/v2-bde07fdceb700b45ea02f16e3bb099e7_1440w.jpg?source=172ae18b
categories: 
- 前端
tags:
- JavaScript
---

## 效果
![](https://img-blog.csdnimg.cn/f60f5db398ef44bf95b51f1cb28e5a79.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_16,color_FFFFFF,t_70,g_se,x_16)
## 代码
```javascript
/**
 * 封装Toast提示
 * @param {提示信息} msg 
 * @param {延迟时间} duration 
 */
function Toast(msg, duration) {
  duration = isNaN(duration) ? 3000 : duration;
  var m = document.createElement('div');
  m.innerHTML = msg;
  m.style.cssText = "font-family:siyuan;max-width:60%;min-width: 150px;padding:0 14px;height: 40px;color: rgb(255, 255, 255);line-height: 40px;text-align: center;border-radius: 4px;position: fixed;top: 50%;left: 50%;transform: translate(-50%, -50%);z-index: 999999;background: rgba(0, 0, 0,.7);font-size: 16px;";
  document.body.appendChild(m);
  setTimeout(function () {
    var d = 0.5;
    m.style.webkitTransition = '-webkit-transform ' + d + 's ease-in, opacity ' + d + 's ease-in';
    m.style.opacity = '0';
    setTimeout(function () {
      document.body.removeChild(m)
    }, d * 1000);
  }, duration);
}
```
