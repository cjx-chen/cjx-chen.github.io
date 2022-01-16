---
title: 【CSS】设置文字不能被选中&解除限制
date:  2022-01-16 20:51:30
img: https://img-blog.csdnimg.cn/img_convert/6a94b39a44d659ccf65af2fd34480ea9.png
categories: 
- 前端
tags:
- CSS
- Javascript
---

## 方法一：JS

```javascript

if (typeof(element.onselectstart) != "undefined") {        
    // IE下禁止元素被选取        
    element.onselectstart = new Function("return false");        
} else {
    // firefox下禁止元素被选取的变通办法        
    element.onmousedown = new Function("return false");        
    element.onmouseup = new Function("return true");        
} 
```

> IE下有 onselectstart 这个方法，通过设置这个方法可以禁止元素文本被选取。而firefox下没有这个方法，但可以通过css或一种变通的办法解决。

另一种方法是：

```javascript
ie:document.selection.empty()
ff:window.getSelection().removeAllRanges()
```
兼容的写法：
```javascript
window.getSelection ? window.getSelection().removeAllRanges() : document.selection.empty();
```
这种方法不但不影响拖放对象的选择效果，还能对整个文档进行清除。

## 方法二：CSS

```css
div {
      -moz-user-select:none;
      -webkit-user-select:none;
      user-select:none;    
}
```
