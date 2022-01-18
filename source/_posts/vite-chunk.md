---
title: 【Vue3】vite打包报错：块的大小超过限制，Some chunks are larger than 500kb after minification
date: 2022-01-18 15:53:58
img: https://pic3.zhimg.com/v2-3b97a39e6f2465dcc2b4718c9a6a8d36_1440w.jpg?source=172ae18b
categories: 
- 安装配置步骤
- 前端
tags:
- Vite
- Vue3
- 报错解决方法
---

## 问题描述
vite打包报错：块的大小超过限制，Some chunks are larger than 500kb after minification：
![](https://img-blog.csdnimg.cn/0ba63b47324e43738240156edb169ba6.png)
## 解决方法
1. 加大限制的大小将500kb改成1000kb或者更大：

```javascript
chunkSizeWarningLimit:1500
```

> build.chunkSizeWarningLimit 类型： number
> 默认： 500
> 块大小警告的限制（以 kbs 为单位）

2. 分解块，将大块分解成更小的块：

```javascript
rollupOptions: {
        output:{
            manualChunks(id) {
              if (id.includes('node_modules')) {
                  return id.toString().split('node_modules/')[1].split('/')[0].toString();
              }
          }
        }
    }
```

> build.rollupOptions
类型： RollupOptions
直接自定义底层 Rollup 包。这与可以从 Rollup 配置文件导出的选项相同，并将与 Vite 的内部 Rollup 选项合并。有关更多详细信息，请参阅汇总选项文档。

![](https://img-blog.csdnimg.cn/318d4a479aba481a88916accd53bdd20.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
## 代码

```javascript
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
// 按需加载
import styleImport from 'vite-plugin-style-import'
import { resolve } from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  base: '/dist/',
  build: {
    chunkSizeWarningLimit:1500,
    rollupOptions: {
        output:{
            manualChunks(id) {
              if (id.includes('node_modules')) {              
                  return id.toString().split('node_modules/')[1].split('/')[0].toString();
              }
          }
        }
    }
  }
})
```
