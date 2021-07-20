---
title: Hexo 搭建个人博客 基础配置及实操
date: 2021-07-20 15:37:15 
img: https://pic2.zhimg.com/v2-7bbe64c2282a997092613d004f0222f2_1440w.jpg?source=172ae18b
categories: 
- 安装配置步骤
tags:
- Hexo
- Git
- Node.js
---

## 初步搭建本地Hexo博客
### 安装
**安装前提**

搭建环境：Windows 10

- Node.js (Node.js 版本需不低于 8.10，建议使用 Node.js 10.0 及以上版本)
- Git

验证成功安装Node.js跟Git，通过查看版本号即可

```bash
node -v
npm-v
```

**安装 Hexo**

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。

不过用 cnpm 更快一点不会有那么多报错，后面我就用 cnpm 了：

```bash
cnpm install -g hexo-cli
```

### 建站
#### 生成项目
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。

```bash
hexo init <项目名称>
```
通过VScode软件打开初始化的博客

#### 运行项目
运行服务：（hexo默认使用4000端口）

```bash
hexo s
```
通过 http://localhost:4000 访问本地hexo服务
![](https://img-blog.csdnimg.cn/20210720145742144.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
## 更换博客主题（hexo-theme-matery）
### 下载
在你的 themes 文件夹下使用 Git clone 命令来下载：

```bash
git clone https://github.com/blinkfox/hexo-theme-matery.git
```

### 更换主题
将博客文件夹下的配置文件_config.yml的主题theme改成：hexo-theme-matery
![](https://img-blog.csdnimg.cn/20210720145925564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
更换完成重新运行服务，主题已成功修改；

## 更换中文
将博客文件夹下的配置文件_config.yml的语言language改为zh-CN
![](https://img-blog.csdnimg.cn/20210720150001170.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
### 修改主题项中的配置
#### 新建分类 categories 页
categories 页是用来展示所有分类的页面，如果在你的博客 source 目录下还没有 categories/index.md 文件，那么你就需要新建一个，命令如下：

```bash
hexo new page "categories"
```
编辑你刚刚新建的页面文件 /source/categories/index.md，至少需要以下内容：

```bash
---
title: categories
date: 2018-09-30 17:25:30
type: "categories"
layout: "categories"
---
```

#### 新建标签 tags 页
tags 页是用来展示所有标签的页面，如果在你的博客 source 目录下还没有 tags/index.md 文件，那么你就需要新建一个，命令如下：

```bash
hexo new page "tags"
```
编辑你刚刚新建的页面文件 /source/tags/index.md，至少需要以下内容：

```bash
---
title: tags
date: 2018-09-30 18:23:38
type: "tags"
layout: "tags"
---
```

#### 新建关于我 about 页
about 页是用来展示关于我和我的博客信息的页面，如果在你的博客 source 目录下还没有 about/index.md 文件，那么你就需要新建一个，命令如下：

```bash
hexo new page "about"
```
编辑你刚刚新建的页面文件 /source/about/index.md，至少需要以下内容：

```bash
---
title: about
date: 2018-09-30 17:25:30
type: "about"
layout: "about"
---
```

#### 新建 404 页
如果在你的博客 source 目录下还没有 404.md 文件，那么你就需要新建一个

编辑你刚刚新建的页面文件 /source/404.md，至少需要以下内容：

```bash
---
title: 404
date: 2018-09-30 17:25:30
type: "404"
layout: "404"
description: "哦吼！完蛋！"
---
```

#### 代码高亮
由于 Hexo 自带的代码高亮主题显示不好看，所以主题中使用到了 hexo-prism-plugin 的 Hexo 插件来做代码高亮，安装命令如下：

```bash
cnpm i -S hexo-prism-plugin
```
然后，修改 Hexo 根目录下 _config.yml 文件中 highlight.enable 的值为 false，并新增 prism 插件相关的配置，主要配置如下：
```bash
highlight:
  enable: false

prism_plugin:
  mode: 'preprocess'    # realtime/preprocess
  theme: 'tomorrow'
  line_number: false    # default false
  custom_css:
```

#### 搜索
本主题中还使用到了 hexo-generator-search 的 Hexo 插件来做内容搜索，安装命令如下：

```bash
cnpm install hexo-generator-search --save
```
在 Hexo 根目录下的 _config.yml 文件中，新增以下的配置项：

```bash
search:
  path: search.xml
  field: post
```

#### 中文链接转拼音（建议安装）
如果你的文章名称是中文的，那么 Hexo 默认生成的永久链接也会有中文，这样不利于 SEO，且 gitment 评论对中文链接也不支持。我们可以用 hexo-permalink-pinyin Hexo 插件使在生成文章时生成中文拼音的永久链接。

安装命令如下：

```bash
cnpm i hexo-permalink-pinyin --save
```
在 Hexo 根目录下的 _config.yml 文件中，新增以下的配置项：

```bash
permalink_pinyin:
  enable: true
  separator: '-' # default: '-'
```

> 注：除了此插件外，hexo-abbrlink 插件也可以生成非中文的链接。

#### 文章字数统计插件（建议安装）
如果你想要在文章中显示文章字数、阅读时长信息，可以安装 hexo-wordcount插件。

安装命令如下：

```bash
cnpm i --save hexo-wordcount
```
然后只需在本主题下的 _config.yml 文件中，将各个文章字数相关的配置激活即可：

```bash
postInfo:
  date: true
  update: false
  wordCount: false # 设置文章字数统计为 true.
  totalCount: false # 设置站点文章总字数统计为 true.
  min2read: false # 阅读时长.
  readCount: false # 阅读次数.
```

#### 添加emoji表情支持（可选的）
本主题新增了对emoji表情的支持，使用到了 hexo-filter-github-emojis 的 Hexo 插件来支持 emoji表情的生成，把对应的markdown emoji语法（::,例如：:smile:）转变成会跳跃的emoji表情，安装命令如下：

```bash
cnpm install hexo-filter-github-emojis --save
```
在 Hexo 根目录下的 _config.yml 文件中，新增以下的配置项：

```bash
githubEmojis:
  enable: true
  className: github-emoji
  inject: true
  styles:
  customEmojis:
```

## Github上搭建博客
### 新建仓库
![](https://img-blog.csdnimg.cn/20210720150551479.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
### 初始化仓库
1. 初始化本地仓库

```bash
git init
```
2. 添加一个远程git地址

```bash
git remote add origin <远程仓库地址>
```

**安装hexo-depoyler-git依赖**

```bash
yarn add hexo-deployer-git
```
**修改部署相关的配置：**

修改 Hexo 根目录下 _config.yml 文件中deploy的相关属性：

```bash
deploy:
  type: git
  repo: <仓库地址>
  branch: master
```

**部署代码**

```bash
cnpm run deploy
```

打开自己的站点看看是否已被部署成功：https://<用户名>.github.io/
![](https://img-blog.csdnimg.cn/20210720151004110.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
## 实现Github自动化部署
由于上面操作中master分支已被占用，我们要把源代码提交到另外一个分支上

**首先 commit 本地代码**

```bash
git add .
git commit -m 'feat: blog init'
```

**切换分支 myblog**
![](https://img-blog.csdnimg.cn/20210720151105790.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
**将 myblog 分支 push 到 github 中**
```bash
git push origin master:myblog
```

**配置 github actions**

在hexo根目录下创建文件deploy.yml，文件路径为：.github/workflows/deploy.yml

文件内容：

```bash
name: Build and Deploy
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v2 # If you're using actions/checkout@v2 you must set persist-credentials to false in most cases for the deployment to work correctly.
        with:
          persist-credentials: false
      - name: Install and Build 🔧 # This example project is built using npm and outputs the result to the 'build' folder. Replace with the commands required to build your project, or remove this step entirely if your site is pre-built.
        run: |
          npm install
          npm run build
        env:
          CI: false
      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@releases/v3
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          BRANCH: master # The branch the action should deploy to.
          FOLDER: pub
```

可能出现下面的bug：

```bash
Error: fatal: No url found for submodule path 'themes/hexo-theme-matery' in .gitmodules
Error: The process '/usr/bin/git' failed with exit code 128
```
解决方案： 

1. 从暂存区删除该文件夹
```bash
git rm --cache themes/hexo-theme-matery
```
2. 把 themes/hexo-theme-matery/.git文件夹删掉；
3. 查看当前状态，并按步骤提交即可：
```bash
git status
git add .
git commit -m "feat: add themes"
git push
```

测试一下 github action 是否生效，修改一下文章内容并提交：
![](https://img-blog.csdnimg.cn/2021072015141961.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
点进去查看：
![](https://img-blog.csdnimg.cn/20210720151435268.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
自此自动化部署已完成。

## 主题的基本配置
### 根目录下的 _config.yml
```bash
title: Wyy's Blog
subtitle: ''
description: ''
keywords: 
author: Wyy   ##博客作者署名
language: zh-CN      ##博客所使用语言，默认`en`
timezone: 'Asia/Shanghai'   ##时区设置
```

> title 所对应的地方，补充：subtitle 所对应的就是博客正中间的subtitle，没有赋值时默认显示subtitle

![](https://img-blog.csdnimg.cn/20210720151807679.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

```bash
theme: matery  ##此处更改为主题的名字，要与themes文件夹下的主题名一致

# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:  ##和git仓库绑定有解释
  type: git
  repo: git@github.com:<用户名>/<用户名>.github.io.git  
  branch: master
```

### themes目录下的_config.yml
**menu，icon，二级菜单**

```bash
menu:
  Index:
    url: /
    icon: fas fa-home
  Tags:
    url: /tags
    icon: fas fa-tags
  Categories:
    url: /categories
    icon: fas fa-bookmark
  Archives:
    url: /archives
    icon: fas fa-archive
  About:
    url: /about
    icon: fas fa-user-circle
  Contact:
    url: /contact
    icon: fas fa-comments
  Friends:
    url: /friends
    icon: fas fa-address-book
```
![](https://img-blog.csdnimg.cn/20210720151941894.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

> 初始效果如上图，当不需要导航栏有这么多标签时，可以选择注释掉不需要的部分。例如：

```bash
menu:
  Index:
    url: /
    icon: fas fa-home
  Tags:
    url: /tags
    icon: fas fa-tags
  # Categories:
  #   url: /categories
  #   icon: fas fa-bookmark
  # Archives:
  #   url: /archives
  #   icon: fas fa-archive
  # About:
  #   url: /about
  #   icon: fas fa-user-circle
  # Contact:
  #   url: /contact
  #   icon: fas fa-comments
  # Friends:
  #   url: /friends
  #   icon: fas fa-address-book
```
![](https://img-blog.csdnimg.cn/20210720152009639.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

> 此时页面上方只显示剩下未被注释的部分

关于每个标签前面的图标，通过icon来设置

```bash
menu:
  Index:
    url: /
    icon: fas fa-home
```
修改 icon 的后半部分，例如，改为
```bash
menu:
  Index:
    url: /
    icon: fas fa-list-ul
```

> 效果如下，具体图标代码点击此处 [传送门](http://www.fontawesome.com.cn/cheatsheet/)

![](https://img-blog.csdnimg.cn/20210720152155308.png)
二级菜单写法如下：

```bash
menu:
  Index:
    url: /
    icon: fas fa-home
    children:
     - name: Musics
       url: /musics
       icon: fas fa-music
     - name: Movies
       url: /movies
       icon: fas fa-film
```
![](https://img-blog.csdnimg.cn/20210720152230243.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
**dream【可选】**

```bash
dream:
  enable: true
  showTitle: true
  title: Dream
  text: Calm down and be yourself
```
![](https://img-blog.csdnimg.cn/20210720152310783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
**indexbtn**

```bash
indexbtn:
  enable: true
  name: CSDN
  icon: fas fa-copyright
  url: https://blog.csdn.net/qq_41376237
```
![](https://img-blog.csdnimg.cn/20210720152339474.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
**sociallink**

```bash
socialLink:
  github:  https://github.com/319226862/wyy
  email: 319226862@qq.com
  facebook: # https://www.facebook.com/xxx
  twitter: # https://twitter.com/xxx
  qq: 319226862
  weibo: # https://weibo.com/xxx
  zhihu: # https://www.zhihu.com/xxx
  rss:  # true、false
```
![](https://img-blog.csdnimg.cn/20210720152405492.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
> 作用如图，其中，不写代表不启用，想添加csdn等其他账号同理

**打赏功能**

```bash
reward:
  enable: true
  title: 你的赏识是我前进的动力
  wechat: /medias/reward/wechat.png
  alipay: /medias/reward/alipay.jpg
```

> 开通功能后，在每篇文章末尾可以通过支付宝或者微信打赏，其中图片保存在/Users/apple/Documents/blog/themes/matery/source/medias/reward 目录下，或者自己选择其他目录保存

**字数统计等**

```bash
postInfo:
  date: true # 发布日期
  update: true # 更新日期
  wordCount: true # 文章字数统计
  totalCount: true # 站点总文章字数
  min2read: true # 文章阅读时长
  readCount: true # 文章阅读次数
```

> 若要开启文章字数统计，需要安装 hexo-wordcount 插件，安装命令:
npm i --save hexo-wordcount
如果使用npm命令不加载或者加载慢，可以使用
cnpm i --save hexo-wordcount

开启后效果：
![](https://img-blog.csdnimg.cn/20210720152546198.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

**featureimages**
```bash
featureImages:
- /medias/featureimages/1.jpg
- /medias/featureimages/2.jpg
- /medias/featureimages/3.jpg
- /medias/featureimages/4.jpg
- /medias/featureimages/5.jpg
- /medias/featureimages/6.jpg
- /medias/featureimages/7.jpg
- /medias/featureimages/8.jpg
- /medias/featureimages/9.jpg
- /medias/featureimages/10.jpg
```
![](https://img-blog.csdnimg.cn/20210720152604311.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

> featureImages 设置的是无文章特色图片时需要显示的文章特色图片，即，发博客是不特定设置博客图片，则从中随机选取一张作为封面

**几何线条背景canvas_nest**

```bash
canvas_nest:
  enable: true
  color: 0,0,255 # 线条颜色, 默认: '0,0,0' ；三个数字分别为(R,G,B)，注意用,分割
  pointColor: 0,0,255 # 交点颜色, 默认: '0,0,0' ；三个数字分别为(R,G,B)，注意用,分割
  opacity: 0.7 # 线条透明度（0~1）, 默认: 0.5
  zIndex: -1 # 背景的 z-index 属性，css 属性用于控制所在层的位置, 默认: -1.
  count: 99 # 线条的总数量, 默认: 99
```
![](https://img-blog.csdnimg.cn/2021072015263564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

> 很多博客都有的几何线条背景
color： 线条颜色
pointColor： 交点颜色
opacity： 线条透明度（0~1）
zIndex： css 属性用于控制所在层的位置,
count： 线条的总数量

**分享链接share**

```bash
sharejs:
  enable: true
  sites: twitter,facebook,google,qq,qzone,wechat,weibo,douban,linkedin
```
![](https://img-blog.csdnimg.cn/20210720152707876.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

> 调整 sites 的顺序即可调整页面的分享图标顺序

**副标题subtitle**

```bash
subtitle:
  enable: true
  loop: true # 是否循环
  showCursor: true # 是否显示光标
  startDelay: 300 # 开始延迟
  typeSpeed: 100 # 打字速度
  backSpeed: 50 # 删除速度
  sub:
    - Calm down and be yourself
    - Just Do 'IT'
```
![](https://img-blog.csdnimg.cn/20210720152736190.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

### 修改导航栏颜色
打开 themes/matery/source/css/matery.css 文件，找到bg-color这个属性，即为导航栏和底部的颜色

```bash
.bg-color {
    background-image: linear-gradient(to right, #8cbfb8 0%, #128c6f 100%);
}
```
![](https://img-blog.csdnimg.cn/20210720152810759.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

> 如上所示，使用的是渐变色，如果不知道要换什么颜色，嫌每次都需要修改再部署比较麻烦，建议在需要换颜色的地方右键->检查，查看这个属性，在控制台对颜色做出相应的更改，满意后再去代码中修改保存。
同理，如果还有其他要修改的位置，相应方法找到元素名称，去css文件中找到并修改

### 个人信息

```bash
profile:
  avatar: /medias/fatcat.jpg
  career: 搬砖人
  introduction: 赚钱养猫养狗!
```

> avatar： 头像设置
career： 职业
introduction： 个人介绍

对应效果图如下：
![](https://img-blog.csdnimg.cn/20210720152912767.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

### 配置"我的项目"信息

```bash
myProjects:
  enable: true
  data:
    hexo-theme-matery:
      icon: fas fa-file-alt
      iconBackground: 'linear-gradient(to bottom right, #66BB6A 0%, #81C784 100%)'
      url: http://github.com/blinkfox/hexo-theme-matery
      desc: This is a Hexo blog theme with 'Material Design' and responsive design.
    Fenix:
        icon: fas fa-database
        iconBackground: 'linear-gradient(to bottom right, #F06292 0%, #EF5350 100%)'
        url: https://github.com/blinkfox/fenix
        desc: 这是 Spring Data JPA 复杂或动态 SQL 查询的扩展库。
    typora-vue-theme:
        icon: fas fa-file-alt
        iconBackground: 'linear-gradient(to bottom right, #29B6F6 0%, #1E88E5 100%)'
        url: https://github.com/blinkfox/typora-vue-theme
        desc: This is a typora theme inspired by Vue document style.
```
![](https://img-blog.csdnimg.cn/20210720152934939.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
```bash
具体自己修改，不想显示，设置enable值为false
```

### 配置"我的技能"信息
```bash
mySkills:
  enable: true
  data:
    html:
      background: 'linear-gradient(to right, #FF0066 0%, #FF00CC 100%)'
      percent: 90%
    css:
      background: 'linear-gradient(to right, #9900FF 0%, #CC66FF 100%)'
      percent: 80%
    javascript:
      background: 'linear-gradient(to right, #2196F3 0%, #42A5F5 100%)'
      percent: 50%
    c/java:
      background: 'linear-gradient(to right, #00BCD4 0%, #80DEEA 100%)'
      percent: 50%
    echart/ps:
      background: 'linear-gradient(to right, #4CAF50 0%, #81C784 100%)'
      percent: 60%
    vue:
      background: 'linear-gradient(to right, #FFEB3B 0%, #FFF176 100%)'
      percent: 30%
```
![](https://img-blog.csdnimg.cn/20210720153013197.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

## Hexo博客发表文章、草稿、添加分类和标签

> 在_post 文件夹下，新建&&.md 文件
基本配置如下：
title： 文章标题
top： 是否把文章置顶
img： 是否给文章定义特色图片，如果不设置，默认从featureimages里面抽取
summary： 是否给文章加上摘要，不设置，默认截取文章开头一部分
categories： 给文章分类
tags： 给文章加标签，可加多个
剩下博客书写同csdn一样，可以直接复制过去

```bash
---
title: hexo的个性化配置
date: 2020-08-31 14:01:19
author: wyy
img: 
top: true
cover: true
coverImg: 
password: 
toc: false
mathjax: false
summary: hexo的matery主题的个性化配置
categories: 
- hexo
tags:
- hexo
---
```

## 常见错误
有时候 push 的时候 git 会突然抽风，报错：
```bash
关于错误:ssh: Could not resolve hostname github.com: Name or service not known.fatal: Could not read from remote repository.
```
我是在终端中输入 `ssh -T git@github.com` 或 `ping github.com` 后再 `push` 就好了。

## 双线部署到 Coding 和 GitHub 并实现全站 HTTPS
### 新建项目
进入 Coding.net 官网，点击个人版登陆，没有账号就注册一个并登录，有团队的就建立一个自己的团队再从里面新建项目，并给其项目新建代码仓库，远程关联 GitHub 上个人博客仓库：
![](https://img-blog.csdnimg.cn/img_convert/5a24686df6e4dc37837992f859082dfd.png)
![](https://img-blog.csdnimg.cn/img_convert/a3bac0da6a1dbb461ba7caeeefacdd9f.png)
### 配置公钥
配置 SSH 公钥方法与 GitHub Pages 的方式差不多，点击你的头像，依次选择【个人账户设置】-【SSH公钥】-【新增公钥】
![](https://img-blog.csdnimg.cn/img_convert/1f2142275fa9d1db6fc6fcf1d0d86027.png)
前面部署到 GitHub Pages 的时候就已经有了一对公钥，我们直接将该公钥粘贴进去就行，公钥名称可以随便写，选中永久有效选项

> 公钥储存位置一般在 C:\Users\用户名\.ssh 目录下的 id_rsa.pub 文件里，用记事本打开复制其内容即可

添加公钥后，我们可以在终端输入以下命令来检查是否配置成功：

```bash
ssh -T git@git.coding.net
```

### 配置 _config.yml
进入你的项目，在右下角有选择连接方式，选择 SSH 方式（HTTPS 方式也可以，但是这种方式有时候可能连接不上，SSH 连接不容易出问题），一键复制，然后打开你本地博客根目录的 _config.yml 文件，找到 deploy 关键字，添加 coding 地址，也就是刚刚复制的 SSH 地址：
![](https://img-blog.csdnimg.cn/img_convert/bde6094d891251bef98826d5bbf5c64d.png)
![](https://img-blog.csdnimg.cn/img_convert/f533d0e28f0a8acc757ead1b74b75de0.png)
添加完成后先执行命令 `hexo clean` 清理一下缓存，然后执行命令 `hexo g -d` 将博客双线部署到 Coding Pages 和 GitHub Pages；

### 网站托管
在项目目录下点击【持续部署】->【网站托管】，按照步骤注册登录腾讯云：
![](https://img-blog.csdnimg.cn/img_convert/f6da7639f8027ccc362e008fd8cdf9d8.png)
最后新建部署网站，仓库地址填 GitHub 上的仓库地址：
![](https://img-blog.csdnimg.cn/img_convert/ae81218c769114a9b43b66823bfb0775.png)
这样就部署成果啦：
![](https://img-blog.csdnimg.cn/img_convert/43f2d5b42a5cdacf5622a380333f3688.png)
点击【访问】即可！

## 将个人博客部署到自己的域名
### 申请域名
我是买了腾讯云个人的域名1年只要1块钱，买完记得实名认证；

### 在仓库里添加CNAME文件并在文件中填写绑定的域名
![](https://img-blog.csdnimg.cn/img_convert/76c09e6b98572421528bfb0a68cfd706.png)
文件里填写的内容：要绑定的域名（不要包含Http://和www）

![](https://img-blog.csdnimg.cn/img_convert/7ee980c63d49b196b0432d187a6ffe3d.png)
### 设置
添加CNAME文件并在文件中填写绑定的域名后应该会自动保存，看看有没有自动保存：
![](https://img-blog.csdnimg.cn/img_convert/68530767be019dec09444475291617a9.png)
### 添加域名解析
ping 你的http://github.io域名，得到一个IP：
![](https://img-blog.csdnimg.cn/img_convert/fdab653e1fc7bcfa6a93e95761a4ba1b.png)
修改你的域名解析记录：
![](https://img-blog.csdnimg.cn/img_convert/f5498b31060943256e1e16bf76efd5e9.png)
添加两个记录，用得到的IP，一个主机记录为：“www”，一个为“@”，
![](https://img-blog.csdnimg.cn/img_convert/016b9e67e91b05b7a7d9a3fd6a78d8ab.png)
这样通过 http://jessieeeeee.xyz/ 就能访问到你的博客了:![](https://img-blog.csdnimg.cn/img_convert/0dae211db5a3012af1b84a0bfa21bde8.png)

