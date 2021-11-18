---
title: 【Vue3】创建 vite + vue3 + Ant Design Vue 项目
date: 2021-11-18 10:51:15
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- 安装配置步骤
- Vue3
tags:
- Vue3
---

## 搭建脚手架

创建项目：
![选择vue](https://img-blog.csdnimg.cn/3297aec083a9472baad4d5be8ce63b37.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![选择vue](https://img-blog.csdnimg.cn/2da1e2db363e4e479595684521588cf6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![创建成功](https://img-blog.csdnimg.cn/0a392c024b1d44b4838522300c96fddc.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
然后按照它的指示运行项目
![打开网址](https://img-blog.csdnimg.cn/9ca3232e836d4e2db831bb0dfb79affe.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![页面如图](https://img-blog.csdnimg.cn/f25c38af1de94c6dac8e9888b7de35ef.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

## 配置文件

安装构建 vue-router：

```powershell
npm i vue-router@next
```

创建 router/index.js 文件：

```javascript
import { createRouter, createWebHistory } from 'vue-router'

const routes = [
  {
    path: '/',
    name: 'Home',
    // 按需加载
    component: () => import('../views/Home.vue')
  }
]

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})

export default router
```

安装构建 vuex

```powershell
npm i vuex@next
```

创建 store/index.js 文件

```javascript
import { createStore } from 'vuex'

export default createStore({
  state: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})
```

在 main.js 中使用 router 和 store:

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

// 挂载实例
const app = createApp(App)
app.use(store)
app.use(router)
app.mount('#app')
```

创建 views/Home.vue 文件：

```html
<template>
  <div class="home">首页</div>
</template>

<script>
  export default {
    name: 'Home',
    components: {},
  };
</script>

<style scoped>

</style>
```

更改 App.vue 文件：

```html
<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>
html, body, #app {
  width: 100%;
  height: 100%;
}
</style>
```

使用 vite 安装 vue3 时，如果使用了 process.env，会遇到 process 未定义的情况，原因是 process.env 已经被移除了。解决办法是在 vite.config.ts 中增加 define：

```javascript
import { defineConfig } from 'vite'
// ...
export default defineConfig({
  // ...
  define: {
    'process.env': {}
  }
})
```
## 搭建脚手架

创建项目：
![选择vue](https://img-blog.csdnimg.cn/3297aec083a9472baad4d5be8ce63b37.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![选择vue](https://img-blog.csdnimg.cn/2da1e2db363e4e479595684521588cf6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![创建成功](https://img-blog.csdnimg.cn/0a392c024b1d44b4838522300c96fddc.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
然后按照它的指示运行项目
![打开网址](https://img-blog.csdnimg.cn/9ca3232e836d4e2db831bb0dfb79affe.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![页面如图](https://img-blog.csdnimg.cn/f25c38af1de94c6dac8e9888b7de35ef.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

## 配置文件

安装构建 vue-router：

```powershell
npm i vue-router@next
```

创建 router/index.js 文件：

```javascript
import { createRouter, createWebHistory } from 'vue-router'

const routes = [
  {
    path: '/',
    name: 'Home',
    // 按需加载
    component: () => import('../views/Home.vue')
  }
]

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})

export default router
```

安装构建 vuex

```powershell
npm i vuex@next
```

创建 store/index.js 文件

```javascript
import { createStore } from 'vuex'

export default createStore({
  state: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})
```

在 main.js 中使用 router 和 store:

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'

// 挂载实例
const app = createApp(App)
app.use(store)
app.use(router)
app.mount('#app')
```

创建 views/Home.vue 文件：

```html
<template>
  <div class="home">首页</div>
</template>

<script>
  export default {
    name: 'Home',
    components: {},
  };
</script>

<style scoped>

</style>
```

更改 App.vue 文件：

```html
<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>
html, body, #app {
  width: 100%;
  height: 100%;
}
</style>
```

使用 vite 安装 vue3 时，如果使用了 process.env，会遇到 process 未定义的情况，原因是 process.env 已经被移除了。解决办法是在 vite.config.ts 中增加 define：

```javascript
import { defineConfig } from 'vite'
// ...
export default defineConfig({
  // ...
  define: {
    'process.env': {}
  }
})
```

运行项目看看

```powershell
npm run dev
```

![运行成功](https://img-blog.csdnimg.cn/311157c742ab4a5c81cdba5961c07081.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![页面如图](https://img-blog.csdnimg.cn/98e2a1f278674481a7a03aa8195f0c29.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

## CSS 重置

在 public 目录下新建一个 css 文件夹，在 public/css 目录下新建 reset.css，把浏览器自主设置的样式去掉；

代码网址：[CSS Tools: Reset CSS](https://meyerweb.com/eric/tools/css/reset/)

```css
/* http://meyerweb.com/eric/tools/css/reset/    v2.0 | 20110126   License: none (public domain)*/html, body, div, span, applet, object, iframe,h1, h2, h3, h4, h5, h6, p, blockquote, pre,a, abbr, acronym, address, big, cite, code,del, dfn, em, img, ins, kbd, q, s, samp,small, strike, strong, sub, sup, tt, var,b, u, i, center,dl, dt, dd, ol, ul, li,fieldset, form, label, legend,table, caption, tbody, tfoot, thead, tr, th, td,article, aside, canvas, details, embed, figure, figcaption, footer, header, hgroup, menu, nav, output, ruby, section, summary,time, mark, audio, video {	margin: 0;	padding: 0;	border: 0;	font-size: 100%;	font: inherit;	vertical-align: baseline;}/* HTML5 display-role reset for older browsers */article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section {	display: block;}body {	line-height: 1;}ol, ul {	list-style: none;}blockquote, q {	quotes: none;}blockquote:before, blockquote:after,q:before, q:after {	content: '';	content: none;}table {	border-collapse: collapse;	border-spacing: 0;}
```

然后在 index.html 的 head 标签中引用：

```html
<link rel="stylesheet" href="./public/css/reset.css">
```

## 安装 Ant Design Vue

在项目目录终端输入一下命令：

```powershell
npm install ant-design-vue@next --save
```

在 main.js 文件中引入：

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import Antd from 'ant-design-vue'
import 'ant-design-vue/dist/antd.css'

const app = createApp(App);
app.config.productionTip = false;

app.use(store)
app.use(router)
app.use(Antd);
app.mount('#app');
```

## 引入本地图片

将图片放置在 src/static 文件中引用即可：
![](https://img-blog.csdnimg.cn/f347861b362940518bdc5c9b38add2b7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_8,color_FFFFFF,t_70,g_se,x_16)
![](https://img-blog.csdnimg.cn/543ae11914fc4378a6bc0a6da389048b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
运行项目看看

```powershell
npm run dev
```

![运行成功](https://img-blog.csdnimg.cn/311157c742ab4a5c81cdba5961c07081.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![页面如图](https://img-blog.csdnimg.cn/98e2a1f278674481a7a03aa8195f0c29.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

## CSS 重置

在 public 目录下新建一个 css 文件夹，在 public/css 目录下新建 reset.css，把浏览器自主设置的样式去掉；

代码网址：[CSS Tools: Reset CSS](https://meyerweb.com/eric/tools/css/reset/)

```css
/* http://meyerweb.com/eric/tools/css/reset/    v2.0 | 20110126   License: none (public domain)*/html, body, div, span, applet, object, iframe,h1, h2, h3, h4, h5, h6, p, blockquote, pre,a, abbr, acronym, address, big, cite, code,del, dfn, em, img, ins, kbd, q, s, samp,small, strike, strong, sub, sup, tt, var,b, u, i, center,dl, dt, dd, ol, ul, li,fieldset, form, label, legend,table, caption, tbody, tfoot, thead, tr, th, td,article, aside, canvas, details, embed, figure, figcaption, footer, header, hgroup, menu, nav, output, ruby, section, summary,time, mark, audio, video {	margin: 0;	padding: 0;	border: 0;	font-size: 100%;	font: inherit;	vertical-align: baseline;}/* HTML5 display-role reset for older browsers */article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section {	display: block;}body {	line-height: 1;}ol, ul {	list-style: none;}blockquote, q {	quotes: none;}blockquote:before, blockquote:after,q:before, q:after {	content: '';	content: none;}table {	border-collapse: collapse;	border-spacing: 0;}
```

然后在 index.html 的 head 标签中引用：

```html
<link rel="stylesheet" href="./public/css/reset.css">
```

## 安装 Ant Design Vue

在项目目录终端输入一下命令：

```powershell
npm install ant-design-vue@next --save
```

在 main.js 文件中引入：

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
import Antd from 'ant-design-vue'
import 'ant-design-vue/dist/antd.css'

const app = createApp(App);
app.config.productionTip = false;

app.use(store)
app.use(router)
app.use(Antd);
app.mount('#app');
```

## 引入本地图片

将图片放置在 src/static 文件中引用即可：
![](https://img-blog.csdnimg.cn/f347861b362940518bdc5c9b38add2b7.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_8,color_FFFFFF,t_70,g_se,x_16)
![](https://img-blog.csdnimg.cn/543ae11914fc4378a6bc0a6da389048b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)