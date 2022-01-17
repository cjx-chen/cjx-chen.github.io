---
title: 【CSS】div层调整z-index属性无效原因分析及解决方法
date:  2022-01-17 20:47:01
img: https://img-blog.csdnimg.cn/img_convert/6a94b39a44d659ccf65af2fd34480ea9.png
categories: 
- 前端
tags:
- CSS
---

## 问题描述
div层调整z-index属性无效；

## 原因分析
在CSS中，只能通过代码改变层级，这个属性就是z-index，要让z-index起作用有个小小前提，就是元素的position属性要是relative，absolute或是fixed。

**z-index无论设置多高都不起作用情况**

这种情况发生的条件有三个：
1. 父标签 position属性为 relative；
2. 问题标签无position属性（不包括static）；
3. 问题标签含有浮动(float)属性。
eg：z-index层级不起作用，浮动会让z-index失效，代码如下:

```html
<div style="position:relative; z-index:9999;">
	<img style="float:left;" src="http://7te9u8.com1.z0.glb.clouddn.com/wp-content/uploads/2014/03/100084691.jpg" alt="div层调整z-index属性无效原因分析及解决方法">
</div>
```
## 解决方法
1. position:relative改为position:absolute；
2. 浮动元素添加position属性（如relative，absolute等）；
3. 去除浮动。

参考资料：[https://blog.csdn.net/LEI2879223426/article/details/69650872](https://blog.csdn.net/LEI2879223426/article/details/69650872)