---
title: Git 的安装与使用
date: 2020-08-31 14:01:19 
img: https://www.leixue.com/uploads/2018/12/Git.jpg!760
categories: 
- 安装配置步骤
tags:
- Git
---

## 目的
通过 git 管理 github 托管项目代码；

## 下载安装
 1. 官网下载：[https://git-scm.com/downloads](https://git-scm.com/downloads)
![](https://img-blog.csdnimg.cn/20200809124239472.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
2. 双击安装
![](https://img-blog.csdnimg.cn/20200809125338428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
3. 选择安装的工作目录
![](https://img-blog.csdnimg.cn/20200809125507588.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
4. 选择组件
![](https://img-blog.csdnimg.cn/20200809125718139.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
5. 开始菜单目录名设置
![](https://img-blog.csdnimg.cn/20200809125801689.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
6. 
![](https://img-blog.csdnimg.cn/20200809125841852.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
7. 选择使用命令行环境
![](https://img-blog.csdnimg.cn/2020080913003894.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
8. 我放弃了，我全选 next 了；
9. 检验是否安装成功：桌面鼠标右键，如有出现两个 git 单词的选项则成功；
 ![](https://img-blog.csdnimg.cn/2020080913052232.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
## 配置 Git 
### 设置全局变量
在桌面鼠标右键打开 git bush here：
![](https://img-blog.csdnimg.cn/20200831134900155.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
输入：
```powershell
$ git config --global user.name "your name" 
$ git config --global user.email "your@email.com"
```
### 登陆 GitHub，创建 SSHkey
然后输入这个，创建 SSHkey：

```powershell
$ ssh-keygen -t rsa -C "your@email.com"
```
然后连续点击三次回车键；
![](https://img-blog.csdnimg.cn/20200831135016735.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
会在本地用户文件夹下生成 .ssh 的文件夹，里面包含 id_rsa 和 id_rsa.pub 两个文件：
![](https://img-blog.csdnimg.cn/20200831135036126.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
然后打开文件夹：
![](https://img-blog.csdnimg.cn/20200831135047998.png#pic_center)
然后用记事本打开id_rsa.pub，全选,复制：
![](https://img-blog.csdnimg.cn/20200831135102411.png#pic_center)
然后我们回到刚刚注册的 GitHub 账号里去，点击设置：
![](https://img-blog.csdnimg.cn/20200831135115308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
然后点击 SSH：
![](https://img-blog.csdnimg.cn/20200831135130934.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
然后点击 NEW SSHkey：
![](https://img-blog.csdnimg.cn/20200831135141520.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
然后把上一步复制的key粘贴进去，添加到GitHub账号设置中：
![](https://img-blog.csdnimg.cn/20200831135152919.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
然后回到 git，输入：
```powershell
$ ssh -T git@github.com
```
最后，输入 `yes`：
![](https://img-blog.csdnimg.cn/20200831135234352.png#pic_center)
好了，这就完成了本地和 GitHub 的通信配置。

## Git 基本工作流程
 
 **Git 工作区域**
![](https://img-blog.csdnimg.cn/20200809131144379.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
**向仓库中添加文件流程**
![](https://img-blog.csdnimg.cn/20200809131255372.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

## Git 初始化及仓库创建和操作
**基本信息设置**

```powershell
# 1.设置用户名
$ git config --global user.name '用户名'

# 2. 设置用户名邮箱
$ git config --global user.email '邮箱'
```
该设置在 github 仓库主页显示谁提交了该文件；

**初始化一个新的 Git 仓库**

在项目目录内初始化 git（创建 git 仓库）；
```powershell
$ cd <项目文件夹>
$ git init 
```
(如果看不见 .git 则设置电脑显示隐藏文件)



## Git 管理远程仓库
### 使用远程仓库
作用：备份，实现代码共享集中化管理；

```powershell
# 在项目目录内初始化 git
$ git init 

# 将远程仓库（github对应的项目）复制到本地
$ git clone <远程仓库地址>

# 对项目进行修改后
$ ...

# 关联远程仓库
$ git remote add origin <远程仓库地址>

# 关联完可以查看一下关联的远程分支
$ git remote -v

# 从已有的分支创建新的分支(如从master分支),创建一个dev分支
$ git checkout -b dev

# 创建完可以查看一下,分支已经切换到dev
$ git branch

# 添加到暂存区
$ git add .

$ git status

# 将文件从暂存区提交到本地仓库
$ git commit -m 'feat: 增加了xx功能'

$ git status

# 获取远程于本地内容同步
$ git pull

# 将本地仓库提交到远程仓库
$ git push -u origin dev	# 将本地的dev分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了
$ git push -u origin master # 将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了
$ git push
```

### Git 克隆操作

 - **目的**：将远程仓库（github对应的项目）复制到本地；
 - **代码**：
```powershell
$ git clone 仓库地址
```

 仓库地址由来：
![](https://img-blog.csdnimg.cn/2020081012392137.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
### 将本地仓库同步到 git 远程仓库中

```powershell
$ git push
```
如果显示`The requested URL returned error: 403 Forbidden while accessing`，则表示没有权限；

一般这种情况是属于私有项目，没有权限，输入用户名密码，或者远程地址采用这种类型：

```powershell
$ vi .git/config

# 将 
# [remote "origin"] 
#	url = https://github.com/用户名/仓库名.git 
# 修改为:
# [remote "origin"]
#	url = https://用户名:密码@github.com/用户名/仓库名.git
```
下面我用 VSCode 中的项目来做一个实例：

首先，先在 github 上新建一个与本地项目相同名字的仓库：
![](https://img-blog.csdnimg.cn/20200831134206510.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
进入如下图页面，记得点下 ssh：
![](https://img-blog.csdnimg.cn/20200831134146528.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
但是目前还不能运行 git bash ,第一次使用 git 的 clone 或者 push 命令时，连接github会出现一个警告，以致出现一个对话：

```powershell
Are you sure you want to continue connecting (yes/no)?
```
因为 git 使用 ssh 连接，而 ssh 连接第一次连接验证 github 服务器 key 时，需要确认 github 服务器 key 的指纹信息是否真的来自于 github 服务器。

所以我们需要取得一个 ssh key，而这一步在前面的 Git 配置中已经讲过了；

所以我们打开以下界面，将代码一行一行复制到 git bash 中：
![](https://img-blog.csdnimg.cn/20200831135453790.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
出现图中的 new branch 就证明执行成功了：
![](https://img-blog.csdnimg.cn/20200831135506814.png#pic_center)
回到 github 的远程仓库界面，刷新，出现你自己的仓库名称证明建立仓库成功了：
![](https://img-blog.csdnimg.cn/20200831135552406.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70#pic_center)
另，在输入 `git remote add origin **************` 时，我报了一个错：

```powershell
fatal: remote origin already exists.（报错远程起源已经存在。）
```
解决办法如下：

```powershell
# 1、先输入 
$ git remote rm origin
# 2、再输入 
$ git remote add origin **************
```

## Git 分支命名规范
git 分支分为集成分支、功能分支和修复分支，分别命名为 develop、feature 和 hotfix，均为单数。
- master（主分支，永远是可用的稳定版本，不能直接在该分支上开发）
- develop（开发主分支，所有新功能以这个分支来创建自己的开发分支，该分支只做只合并操作，不能直接在该分支上开发）
- feature-xxx（功能开发分支，在develop上创建分支，以自己开发功能模块命名，功能测试正常后合并到develop分支）
- feature-xxx-fix(功能bug修复分支，feature分支合并之后发现bug，在develop上创建分支修复，之后合并回develop分支。PS:feature分支在申请合并之后，未合并之前还是可以提交代码的，所以feature在合并之前还可以在原分支上继续修复bug)
- hotfix-xxx（紧急bug修改分支，在master分支上创建，修复完成后合并到 master）

> 注意事项：
一个分支尽量开发一个功能模块，不要多个功能模块在一个分支上开发。
feature 分支在申请合并之前，最好是先 pull 一下 develop 主分支下来，看一下有没有冲突，如果有就先解决冲突后再申请合并。

## Commit message 的格式
### type
用于说明 commit 的类别，只允许使用下面7个标识。

- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动

> 如果type为feat和fix，则该 commit 将肯定出现在 Change log
> 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。


## Github Pages 搭建网站
### 个人站点
####  访问
https://用户名.github.io

####  搭建步骤

 1. 创建个人站点 -> 新建仓库（注：仓库名称必须是`用户名.github.io`）；
![](https://img-blog.csdnimg.cn/20200810134029328.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
 2. 在仓库下新建 index.hitml 的文件即可；
![](https://img-blog.csdnimg.cn/20200810134202264.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
![](https://img-blog.csdnimg.cn/20200810134245835.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
![](https://img-blog.csdnimg.cn/20200810134331223.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

> 1. github pages 仅支持静态网页；
> 2. 仓库里面仅能是 html 文件；

然后我失败了：
![](https://img-blog.csdnimg.cn/20200810135459734.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
不知道为啥，害；

### Project Pages 项目站点
####  访问
https://用户名.github.io/仓库名
####  搭建步骤

 1. 进入项目主页，点击 settings；
 2. 在 settings 页面，点击 【Choose a theme】来自动生成主题页面：
![](https://img-blog.csdnimg.cn/20200810135928400.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
然后我的页面一直加载不出来，气死我了，就先写到这里吧；

————————————————————————
参照了两篇知乎文：

 - [2018-06-30 菜鸟心得之如何将 vscode 与 github 连接实现文件推送](https://zhuanlan.zhihu.com/p/38776323?utm_source=wechat_session&utm_medium=social&utm_oi=1136270670114693120)
 - [在 VScode 上配置 Git](https://zhuanlan.zhihu.com/p/31417255?utm_source=wechat_session&utm_medium=social&utm_oi=1136270670114693120)

> 以上步骤中的图片大部分是引用自这两篇文章，而本人亲自尝试后，最后成功的结果图片是截自自己尝试的结果；

