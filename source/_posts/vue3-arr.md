---
title: 【Vue3】使用reactive包裹数组赋值
date:  2022-01-17 12:43:31
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- Vue3
tags:
- Vue3
- Javascript
---

## 需求
将接口请求到的列表数据赋值给响应数据arr


## 代码
```javascript
const arr = reactive([]);

const load = () => {
  const res = [2, 3, 4, 5]; //假设请求接口返回的数据
  // 方法1 失败，直接赋值丢失了响应性
  // arr = res;
  // 方法2 这样也是失败
  // arr.concat(res);
  // 方法3 可以，但是很麻烦
  res.forEach(e => {
    arr.push(e);
  });
};
```

> 方法1：vue3 使用 proxy，对于对象和数组都不能直接整个赋值；
> 方法2：concat 不改变原数组

```javascript
// 方法4
const state = reactive({
  arr: []
});
state.arr = [1, 2, 3]

// 方法5
const state = ref([])
state.value = [1, 2, 3]

// 方法6
const arr = reactive([])
arr.push(...[1, 2, 3])
// 亦或者
arr.length = 0 // 清空原数组
arr.push(...res) // 解构然后push进去
```
