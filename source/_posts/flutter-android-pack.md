---
title: flutter 安卓打包步骤
date: 2021-01-08 10:55:12
img: https://pic2.zhimg.com/v2-d4475f94d92ae6012a4f2f727a51700d_1440w.jpg?source=172ae18b
categories: 
- 安装配置步骤
- flutter
tags:
- flutter
- Android
---

## 更改 App 图标
首先，就是 App 的图标问题，在以下这几个部分把图标改完即可（文件命名要一样）：
![](/api/project/9123846/files/24428316/imagePreview)
别忘了改图标的引用设置：
![](/api/project/9123846/files/24428319/imagePreview)

## 更改 App 名称
然后就是 App 的名字：
![](/api/project/9123846/files/24428336/imagePreview)

## 生成 keystore
下一步就是生成 keystore，这里的坑挺多的，官方写的非常简单，只要在终端运行如下代码就可以成功,但事实是报错：
```
keytool -genkey -v -keystore ~/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
根本找不到这个目录，真的很坑，其实我们只是没有配置环境变量。但是为了一个包配置环境变量是不值得的；【但我配置了哈哈哈】

这时候可以用下面的命令找到 keytool.exe 的位置：
```
flutter doctor -v
```
这里我们要找的其实就是这个 java 地址：
![](/api/project/9123846/files/24428365/imagePreview)
这时候你直接拷贝命令并进行输入，但这里也有个坑，就是如果文件夹中间带有空空，你需要用带引号扩上，例如：
```
D:\Program\Android\'Android Studio'\jre\bin\keytool -genkey -v -keystore ~/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
但是我没有，我应该是这样：
```
C:\Users\86135\Downloads1\jre\bin\keytool -genkey -v -keystore ~/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
但是我因为配置了环境，所以我是这样：
```
keytool -genkey -v -keystore ~/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
这就可以了吗？那你就太天真了，还是会报错：
![](/api/project/9123846/files/24428381/imagePreview)
这个错误的主要问题是目录不存在和没有写权限，所以我们要更换一个有写权限的目录。我们把命令改成了下面的形式：
```
C:\Users\86135\Downloads1\jre\bin\keytool -genkey -v -keystore D:/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
配置了环境的直接：
```
keytool -genkey -v -keystore D:/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
这时候就可以创建成功了。你的D盘下面就会有一个Jks的文件，记住这个文件不能共享给任何人。
![](/api/project/9123846/files/24428386/imagePreview)
有了这个 key.jks 文件后，可以到项目目录下的 android 文件夹下，创建一个名为 key.properties 的文件，并打开粘贴下面的代码：
```
storePassword=<password from previous step>    //输入上一步创建KEY时输入的 密钥库 密码
keyPassword=<password from previous step>    //输入上一步创建KEY时输入的 密钥 密码
keyAlias=key
storeFile=<E:/key.jks>    //key.jks的存放路径
```
我的文件最后是这样的：
```
storePassword=123123
keyPassword=123123
keyAlias=key
storeFile=D:/key.jks
```
这个工作中也不要分享出去哦，这个Key就算生成成功了。

## 配置 key 注册
key生成好后，需要在build.gradle文件中进行配置。这个过程其实很简单，就是粘贴复制一些东西，你是不需要知道这些文件的具体用处的。

第一项：

进入项目目录的 /android/app/build.gradle 文件，在 android{ 这一行前面,加入如下代码：
```
def keystorePropertiesFile = rootProject.file("key.properties")
def keystoreProperties = new Properties()
keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
```
![](/api/project/9123846/files/24428405/imagePreview)
把如下代码进行替换：
![](/api/project/9123846/files/24428408/imagePreview)
替换成的代码：
```
signingConfigs {
    release {
        keyAlias keystoreProperties['keyAlias']
        keyPassword keystoreProperties['keyPassword']
        storeFile file(keystoreProperties['storeFile'])
        storePassword keystoreProperties['storePassword']
    }
}
buildTypes {
    release {
        signingConfig signingConfigs.release
    }
}
```

## 生成 apk
直接在终端中输入 flutter build apk 就打包成功了，我们可以直接在终端输入 flutter install 让 apk 安装在虚拟机上；
![](/api/project/9123846/files/24428423/imagePreview)
这样则是成功：
![](/api/project/9123846/files/24428425/imagePreview)
生成成功后即可在 build -> app -> outputs -> apk 文件夹中获取最终打包出来的 apk 文件安装试用：
![](/api/project/9123846/files/24428428/imagePreview)