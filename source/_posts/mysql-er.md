---
title: 【MySQL】数据表自动生成ER图
date: 2022-01-17 12:11:58
img: https://www.xuekebaba.com/uploads/202002/24/200224124159340.jpg
categories: 
- 数据库
tags:
- MySQL
---

## 环境
mysql workbench

## 步骤
1.  通过菜单栏 ”Database”，选择“Reverse Engineer…”，输入连接信息，并一路Next；
![](https://img-blog.csdnimg.cn/2b97178094a0488a82e64cedffced944.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
2. 选择要生成ER图的数据库：
![](https://img-blog.csdnimg.cn/3e2241fac98946b3a4ab36ca82e9bb57.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
3. 一路Next，最后excute和close；
4. 可以看到，在ERR Diagram区域多了一张图，点击它，就看到了自己想要的ER图了：
![](https://img-blog.csdnimg.cn/d5c625811a7b4e769b4613f2ecf7d0d2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
5. 导出到图片：
![](https://img-blog.csdnimg.cn/9028fa38d59845b8a93b351d47c56f32.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

