---
title: 【SQL Server】Win10 安装 SQL Server 2008 与使用指南
date: 2021-09-24 17:08:02
img: https://img0.baidu.com/it/u=1411725596,3589009048&fm=26&fmt=auto
categories: 
- 安装配置步骤
- SQL Server
tags:
- SQL Server
---

## 背景

某喵学校学的是SQL Server 2008 R2，我学的是MySQL 2018，他找我 debug 的时候可能多少有点差别，就下了一个方便实操试试；

昨天他正常建表，设了联合主键之后正常插入数据报错如下：`"违反了 PRIMARY KEY 约束 'PK_SC2'.不能在对象 'dbo.SC2' 中插入重复键."`。我用相同步骤试了一下，发现没有问题，只好劝他重装（我很抱歉，但是重装大法好！

## 简介

SQL Server 系列软件是 Microsoft 公司推出的关系型数据库管理系统。2008年10月，SQL Server 2008 简体中文版在中国正式上市，SQL Server 2008 版本可以将结构化、半结构化和非结构化文档的数据直接存储到数据库中。可以对数据进行查询、搜索、同步、报告和分析之类的操作。数据可以存储在各种设备上，从数据中心最大的服务器一直到桌面计算机和移动设备，它都可以控制数据而不用管数据存储在哪里。

## 安装步骤

1. 登陆微软中国官网：**Microsoft - Official Home Page**；在搜索中输入 **SQL Server 2008** 并搜索。
   ![](https://img-blog.csdnimg.cn/7d17b78f84504bde91b76bab427a3b3e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
   (16, 11, 19)最近微软的中文官网不知何故，会搜不到 SQL Server 2008，我直接把下载链接放到这里了

[Download Microsoft® SQL Server® 2008 R2 SP2 - Express Edition from Official Microsoft Download Center](https://www.microsoft.com/zh-CN/download/details.aspx?id=30438)

2. 选择你要下载的版本，不用犹豫，第一个就是。我们下载的这个版本全称是：**Microsoft® SQL Server® 2008 R2 SP2 - Express Edition**，确认后点击进入
   ![](https://img-blog.csdnimg.cn/a044720c18a6474c8bd21792c0304564.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
3. 选择你要的语言，点击下载 (想要安装别的语言也可以，但是得安装相应的语言包，建议初学者还是默认的中文好了) 
   ![](https://img-blog.csdnimg.cn/cb5ae08efd8f4127b9d6060f5686b35e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
   点了下载后你会发现弹出下面的页面
   ![](https://img-blog.csdnimg.cn/232b486464a7439c99f2b8c6d0491ade.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
   这里有很多供你下载，我们只选择**两个**：SQLEXPR_x64_CHS.exe 和 SQLManagementStudio_x64_CHS.exe

> PS.如果你是32位系统就选择x86的（9102年了，应该都是64位的了吧）

选中后下载到你经常保存文件的地方即可（这个地方并不是sql要安装的地方）。

全部下载后如图所示：
![](https://img-blog.csdnimg.cn/167d8659b30c40c89b7f9b013b4ca0e6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_19,color_FFFFFF,t_70,g_se,x_16)

4. 正式安装：先安装SQL，再安装 SQL Management Studio

双击SQLEXPR_x64.CHS
![等待加载完毕](https://img-blog.csdnimg.cn/4cee8b6299d04a5a950c0a7273ee8e5c.png)
（这时会有一定的几率提醒你的电脑缺少Microsoft .NET Framework 2.0 或更高版本，根据他的提示进行安装就行）
![](https://img-blog.csdnimg.cn/4104037f8ff04bd78eae9c0567ce58a6.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
如果没有，请忽略这一步。

当他顺利加载完毕之后，我们就可以看到下图所示的界面

![点击全新安装](https://img-blog.csdnimg.cn/ee7460d5d3144ef79db4ea24d8f41191.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![接受并下一步](https://img-blog.csdnimg.cn/6a62235c4790483fbfde0cf9a9db54ef.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![点击安装](https://img-blog.csdnimg.cn/1df316e51499416dbecb1ce0f7601be8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
一直下一步，保持默认设置到”实例配置“这一节，并选择”默认实例“，并点击下一步
![](https://img-blog.csdnimg.cn/a463b21f64c642d3b859adb2814fd2ca.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
再一路下一步到“数据库引擎配置”这一节
![如果没有用户的话就点击“添加当前用户”](https://img-blog.csdnimg.cn/8f457ee40dd34d82988de8ff0f2e607a.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![错误报告可选可不选](https://img-blog.csdnimg.cn/40cbdb303daa4056b2394ef78627049d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
一直下一步直到安装完成
![](https://img-blog.csdnimg.cn/0a99304716fc4839ac850dfca905c462.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
到此为止，我们的安装过程已经进行了 1/2 了，还剩下一个 management studio 没有安装；大家可能发现安装过程十分简单，其实就是就是这么简单，除了极个别需要注意的，**一路下一步就没错**！

接下来安装 SQL Management Studio

一样地，双击 SQLManagementStudio_x64_CHS.exe
![](https://img-blog.csdnimg.cn/1c822a5f55df4c7f88e660d71a84ef07.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
等待安装界面弹出（和第一个安装的界面没啥不同，但里面不一样）
![选择全新安装（是默认选项）](https://img-blog.csdnimg.cn/968336e81d174dfaa3931a8c93b95b03.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![接受并下一步](https://img-blog.csdnimg.cn/04942190a81f4821aac6c1b41841f018.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![默认全选并下一步](https://img-blog.csdnimg.cn/f15e8c3d51cd432b8cfd3dfdc0f9b6f5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![同样可选可不选的错误报告](https://img-blog.csdnimg.cn/6eeb986bfec449049e881ce5ef68259f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
一直下一步，下一步……直到安装完成。
![SQL Management Studio也成功安装了](https://img-blog.csdnimg.cn/b5159b24d4ae48c8bbacd07aa3fbdfd2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

5. 启动和使用

单击左下角的 win 标志，找到 SQL Management Studio 并双击启动
![](https://img-blog.csdnimg.cn/4e0306ab87e9493ca634659b1cd9c939.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
第一次启动的时候会提示这个，无妨
![](https://img-blog.csdnimg.cn/5d344ac8ad6d4b4ebf3fa4221eebea08.png)
启动成功后会出现如图所示的界面
![](https://img-blog.csdnimg.cn/3f7afbb0d4c749379b6485ec22155bba.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
点击连接，服务器名称默认就好（是你电脑的名称）

连接成功后就会看到
![](https://img-blog.csdnimg.cn/6e254363d228419db19deeef71956c9b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
**安装完全成功！**

## 建库建表使用指南

1. 右击数据库，选择第一个，新建一个数据库；
   ![](https://img-blog.csdnimg.cn/fe74264cceb146e0a4392fea051af9bd.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_11,color_FFFFFF,t_70,g_se,x_16)
   ![输入数据库名字之后点击确定](https://img-blog.csdnimg.cn/d4367fb6702e4b97842bde0e80f4cf10.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
   此时数据库已经生成但其中没有表
   ![](https://img-blog.csdnimg.cn/5e22a46693fd404180b42cf1974ee1d2.png)
2. 右击表建立一个表填写自己要写的字段；
   ![](https://img-blog.csdnimg.cn/cea6013c93c444ff9225976ff255f95b.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_12,color_FFFFFF,t_70,g_se,x_16)
   ![填好所需字段之后shift选中目标字段右键设置联合主键](https://img-blog.csdnimg.cn/81be7abf588b4f99af8f97c24dc92f92.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
   然后 Ctrl + S 保存设置表名：
   ![点击确定](https://img-blog.csdnimg.cn/b72b03588b054ab791d4e11d17d29ee8.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_16,color_FFFFFF,t_70,g_se,x_16)
3. 插入数据：对 dbo.SC 右击选择编辑前200行，进入操作页面
   ![](https://img-blog.csdnimg.cn/8854c4e0464f4e9189e696d9ba725fd2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_16,color_FFFFFF,t_70,g_se,x_16)
   插入所需数据之后右键执行
   ![](https://img-blog.csdnimg.cn/f2d330232c9d4ba1aa04f48854f0b6b9.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
4. 查看数据：对 dbo.SC 右击选择选择前1000行
   ![](https://img-blog.csdnimg.cn/2567d12668634077bc574429a027fdc5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_15,color_FFFFFF,t_70,g_se,x_16)
   ![查询执行成功](https://img-blog.csdnimg.cn/e43d9d129d2246f9a653f44c04c34d27.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

