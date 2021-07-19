---
title: Node.js 的安装及环境配置
date: 2021-01-04 11:12:07
img: https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fpic3.zhimg.com%2Fv2-682ae23854d349a0f1e27b80940a32c0_1200x500.jpg&refer=http%3A%2F%2Fpic3.zhimg.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1629292271&t=47e2a6cba9b0c8b3d4f103847dca6303
categories: 
- 安装配置教程
tags:
- Node.js
---

# 安装 Node.js 步骤
1. 下载对应你系统的 Node.js 版本：[https://nodejs.org/en/download/](https://nodejs.org/en/download/)
2. 选安装目录进行安装
3. 环境配置
4. 测试

# 前期准备
1. Node.js 简介
简单的说 Node.js 就是运行在服务端的 JavaScript。Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境。Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效。Node.js 的包管理器 npm，是全球最大的开源库生态系统。

2. 下载 Node.js
打开官网下载链接：[https://nodejs.org/en/download/](https://nodejs.org/en/download/) ：
![](https://img-blog.csdnimg.cn/20210104105419256.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
# 开始安装
1. 下载完成后，双击开始安装 Node.js：
![](https://img-blog.csdnimg.cn/20210104105505625.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
然后就一直点 Next 就可以啦；
2. 在键盘按下【win+R】键，输入 cmd，然后回车，打开 cmd 窗口：
![](https://img-blog.csdnimg.cn/20210104105755741.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
# 环境配置
说明：这里的环境配置主要配置的是npm安装的全局模块所在的路径，以及缓存cache的路径，之所以要配置，是因为以后在执行类似：npm install express [-g] （后面的可选参数-g，g代表global全局安装的意思）的安装语句时，会将安装的模块安装到【C:\Users\用户名\AppData\Roaming\npm】路径中，占C盘空间。

1. 在 nodejs 安装路径下新建如下两个文件夹：
① node_global：用来存放全局模块
② node_cache：用来存放下载包的缓存。
![](https://img-blog.csdnimg.cn/20210104110404710.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
2. 打开终端输入如下两条命令，运行：
```powershell
# 设置全局模块存放路径
npm config set prefix "C:\Program Files\nodejs\node_global" 
# 设置缓存文件夹
npm config set cache "C:\Program Files\nodejs\node_cache" 
```
![](https://img-blog.csdnimg.cn/20210104110824434.png)

> 说明：新建以上两个文件夹，可以避免日后项目中使用
> npm下载全局模块的时候，安装在C:\Users\username\AppData\下的Roaming\npm下，太占空间！
3. 配置环境变量：
在环境变量 -> 系统变量中新建一个变量名为 “NODE_PATH”， 值为“C:\Program Files\nodejs\node_modules”，如下图：
![](https://img-blog.csdnimg.cn/20210104111930863.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
4. 最后编辑用户变量里的Path，将相应npm的路径改为：D:\Program Files\nodejs\node_global，如下：
更改前：
![](https://img-blog.csdnimg.cn/20210104112111290.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
更改后：
![](https://img-blog.csdnimg.cn/20210104112201505.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
配置完成。


