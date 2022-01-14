---
title: 【Vue3】保留小数点位数以及转化为百分比
date:  2022-01-14 16:32:41
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- Vue3
tags:
- Vue3
- Javascript
---

**toFixed [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed)**
toFixed() 方法使用定点表示法来格式化一个数值。

一、保留小数点后两位四舍五入

```javascript
export function NumFilter (value) {
  // 截取当前数据到小数点后两位
  let realVal = parseFloat(value).toFixed(2)
  return realVal
}
```

二、保留两位小数不四舍五入

```javascript
export function numFilter (value) {
  // 截取当前数据到小数点后三位
  let tempVal = parseFloat(value).toFixed(3)
  let realVal = tempVal.substring(0, tempVal.length - 1)
  return realVal
}
```
三、将小数转化为百分比（保留两位小数，四舍五入）

```javascript
export function ChangeDecimalToPercentage(data) {
  let data1 = (data*100).toFixed(2)+"%"
  return data1
}
```

> 注意：将小数转化为百分比时，必须使用.toFixed()保留需要的位数，否则会默认多出很多小数。
