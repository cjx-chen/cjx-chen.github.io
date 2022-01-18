---
title: 【JavaScript】清空数组的三种方式
date: 2022-01-18 16:53:22
img: https://pic1.zhimg.com/v2-bde07fdceb700b45ea02f16e3bb099e7_1440w.jpg?source=172ae18b
categories: 
- 前端
tags:
- JavaScript
---

## 方式1，splice

```javascript
var ary = [1,2,3,4];
ary.splice(0,ary.length);
console.log(ary); // 输出 []，空数组，即被清空了
```
## 方式2，length赋值为0

这种方式很有意思，其它语言如Java，其数组的length是只读的，不能被赋值。如：

```javascript
int[] ary = {1,2,3,4};
ary.length = 0;
```
Java中会报错，编译通不过。而JS中则可以，且将数组清空了。

```javascript
var ary = [1,2,3,4];
ary.length = 0;
console.log(ary); // 输出 []，空数组，即被清空了
```
目前 Prototype中数组的 `clear` 和mootools库中数组的 `empty` 使用这种方式清空数组。  
## 方式3，赋值为[]
```javascript
var ary = [1,2,3,4];
ary = []; // 赋值为一个空数组以达到清空原数组
```
这里其实并不能说是严格意义的清空数组，只是将ary重新赋值为空数组，之前的数组如果没有引用在指向它将等待垃圾回收。

Ext库Ext.CompositeElementLite类的 `clear` 使用这种方式清空。

> 方式2 保留了数组其它属性，方式3 则未保留。很多人认为方式2的效率很高些，因为仅仅是给length重新赋值了，而方式3则重新建立个对象。经 测试 恰恰是方式3的效率高。

## 测试代码

```javascript
var a = [];
for (var i=0; i< 1000000; i++){
    a.push(i);
}
var start = new Date();
//a = [];
a.length = 0;
var end = new Date();
alert(end - start);
```
测试结果：
![](https://img-blog.csdnimg.cn/0792c8a46c4d426282e5fc0abb91454e.png)
以上结果可看到：方式3更快，效率更高。因此如果不保留原数组的其它属性Ext采用的方式更值得推荐。
