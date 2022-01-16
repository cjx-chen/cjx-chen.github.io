---
title: 【Vue3】实现动态给id赋值，点击事件获取当前点击的元素的id操作
date:  2022-01-16 20:24:05
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- Vue3
tags:
- Vue3
- Html
- Javascript
---

## 场景
需要让输出的 id 为 0，1……

## 代码

```html
<div v-for="(item,index) in list" :key="index" >
	<div :id="index" @click="b(index)">我是id</div>
</div>
```
然后在 vue 的实例中就可以拿到对应的 id

```javascript
b(index){
    this.list.splice(index,1);
}
```

或

```html
<div @click="open($event)" id="1">添加<div>
```

```javascript
open(a){
  console.log(a.currentTarget.id)//1
}
```
