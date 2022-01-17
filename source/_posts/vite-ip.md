---
title: 【Vue3】vite 配置IP，解决“vite use `--host` to expose”
date: 2022-01-17 20:55:09
img: https://pic3.zhimg.com/v2-3b97a39e6f2465dcc2b4718c9a6a8d36_1440w.jpg?source=172ae18b
categories: 
- 安装配置步骤
- 前端
tags:
- Vite
- Vue3
---

## 问题描述
vite 启动后出现 `“ Network: use --host to expose ”`

```shell
vite v2.3.7 dev server running at:

  > Local: http://localhost:3000/
  > Network: use `--host` to expose
```

## 原因分析
这是因为IP没有做配置，所以不能从IP启动，需要在 vite.config.js做相应配置；

## 解决方法
在 vite.config.js中添加 server.host 为 0.0.0.0：

```javascript
export default defineConfig({
    plugins: [vue()],
    // 在文件中添加以下内容
    server: {
        host: '0.0.0.0'
    }
})
```
保存后显示：

```shell
vite v2.3.7 dev server running at:

  > Network:  http://192.168.199.127:3000/
  > Local:    http://localhost:3000/
```
