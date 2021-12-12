---
title: 【Apache】Web 服务器配置与 FTP 服务器配置
date: 2021-12-13 00:12:54
img: http://geode.incubator.apache.org/img/asf_logo.png
categories: 
- 安装配置步骤
tags:
- Apache
- ftp
---

## 设置端口号为：8080，查看访问方式有何区别
打开 Apache 的配置文件 httpd.conf：
![点开http.conf](https://img-blog.csdnimg.cn/50fb3910977041b3ba28f7d07853f180.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
搜索 listen：
![搜索listen](https://img-blog.csdnimg.cn/e402b3fb547044f48fbe517e7ef106a1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
将端口号改为 `8080`，然后重启 Apache，我们发现：

之前打开的网址是 localhost：
![之前打开的网址是localhost](https://img-blog.csdnimg.cn/e5abef619dff465ba062969920ebe436.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
现在打开的网址是 localhost:8080：
![现在打开的网址是localhost:8080](https://img-blog.csdnimg.cn/a2a272fade8143b4b910277f5ae41c6d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
## 将文档主目录放到 d:\homepage 文件夹下
打开 Apache 的配置文件 httpd.conf 找到了 `DocumentRoot "D:/Download/xampp/htdocs"`与 `<Directory "D:/Download/xampp/htdocs">` ![搜索htdocs](https://img-blog.csdnimg.cn/59712151df9b40b29a8f6fb3973f92b3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
改为 `DocumentRoot "D:/homepage"` 与 `<Directory "D:/homepage">`
![修改主目录地址](https://img-blog.csdnimg.cn/b0164e7a0f4847fabdd31c1a643bea64.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
这时候重启 Apache 试一下，会发现首页出来了：
![index.html](https://img-blog.csdnimg.cn/168680837a6b42c5ac873fde1af6b757.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

## 设置 default.htm 为缺省的访问文件
“缺省 意思即“默认”。 缺省文件名 系统默认的文件名。也就是说你没有指定用哪件工具，系统自动提供给你的那个就是缺省的，例如你在打开网页时，如果IE是缺省的浏览器，系统就会打开IE——Internet Explorer，使用IE来浏览网页。 

在 Apache 的配置文件 httpd.conf 中搜索 `DirectoryIndex`：
![可以看到 default.htm 已被设为缺省的访问文件](https://img-blog.csdnimg.cn/c4ab454af90c49beb1e2675eec989ca6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

## 为 d:\web2002 文件夹， 设置虚拟目录名 \st2002
在 Apache 的配置文件 httpd.conf 中搜索 `<IfModule alias_module>`：
![搜索 <IfModule alias_module>](https://img-blog.csdnimg.cn/efba0383806240e2a1b78d34a8792d56.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
在里面添加：`Alias /st2002 "d:/web2002/"`：
![添加虚拟目录配置](https://img-blog.csdnimg.cn/5acee0c0da8347d8952291fe755aa1d7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
然后在`</IfModule>` 后面接着加：
![添加如图代码](https://img-blog.csdnimg.cn/cc2748ef0f6b495b9c90fcff1b59907d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
保存后，重新启动 Apache 就可以了。

## 取消 st2002 的目录浏览功能
在上文添加的代码中，将 Options 进行如下修改：
![修改 Options](https://img-blog.csdnimg.cn/809e3ccf27db44a78a3e2cf22f6ce079.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
可关闭 Apache 相关目录的浏览功能。

## 用 www 的 upload 上传文件到 d:\web2002 文件夹，用 ftp 复制文件到 d:\web2002 文件夹，比较操作上的区别
### 配置 放上传文件的目录 apache(httpd)
修改 apache vhost 配置文件：D:\Download\xampp\apache\conf\extra\httpd-vhosts.conf，添加以下配置：

```powershell
<VirtualHost *:8080>
     ServerAdmin Administrator@www.mediamix.cn
     DocumentRoot "D:/web2002"
     ServerName www.mediamix.cn
     ServerAlias www.mediamix.cn
     ErrorLog "logs/mediamix.cn-error.log"
     CustomLog "logs/mediamix.cn.log" common
    <Directory "D:/web2002">
      Options Indexes FollowSymLinks Includes ExecCGI
      AllowOverride All
      Require all granted
    </Directory>
</VirtualHost>
```
（这一步好像并没有起到什么作用？

### www 文件上传
将 d:/homepage/index.html 的内容改为以下代码：

```html
<html>
       <head>
           <meta charset="utf-8"/>
           <title>文件上传表单</title>
       </head>
       <body>
           <table>
               <form enctype='multipart/form-data' name='myform' action='submit.php' method='post'>
                   <input type="hidden" name="MAX_FILE_SIZE" value="1000000000"/>
                  <tr><td>选择文件上传
                          <input name='rzfile' type='file'/>
                  </td></tr>
                  <tr><td colspan='2'>
                          <input name='submit' value='上传' type='submit'/>
                  </td></tr>
              </form>
          </table>
          </body>
 </html>
```
将 d:/homepage/index.php 的内容改为以下代码：

```php
<?php
  //header('content-type:test/html;charset=utf-8');
 //1.通过$_FILES文件上传变量接收上传文件信息
 print_r($_FILES);
   $file=$_FILES['rzfile'];
   $filename=$file['name'];
   $type=$file['type'];
   $tmp_name=$file['tmp_name'];
   $size=$file['size'];
  $error=$file['error'];
  $uploaddir='/upload/';
  $uploadfile=$uploaddir.basename($filename);
 
  //2.判断错误号，只有为0或者是UPLOAD_ERR_OK，表示没有错误发生，上传成功
  if($error == UPLOAD_ERR_OK) {
      if(move_uploaded_file($tmp_name, $uploadfile)) {
         echo 'file:'.$filename.'upload successful';
     }
     else {
         echo 'file'.$filename.'upload failed';
     }
  }else{
     switch($error) {
     case 1:
        echo '1: upload file size beyond upload_max_filesize';
        break;
   case 2:
        echo '2: upload file size beyond post form MAX_FILE_SIZE limit';
        break;
    case 3:
          echo '3: 文件被部分上传';
        break;
     case 4:
     echo '4: 没有选择上传文件';
     break;
   case 6:
       echo '6: 没有找到临时目录';
         break;
    case 7:
     case 8:
         echo '7:8: 系统错误';
         break;
    }
 }
 ?>
```
然后进行一次文件上传：
![选择文件，点击上传](https://img-blog.csdnimg.cn/ea3ab839e9ac44a2bf565b16ce39afba.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![上传成功](https://img-blog.csdnimg.cn/060370393276435684fb1b580449652f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
查看 d:/web2002，有我们上传的 test2.txt 文件，即成功：
![上传成功](https://img-blog.csdnimg.cn/8c53689961ed4756a8822ec3421f796c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
### 匿名 FTP 配置
![点击admin开启ftp服务](https://img-blog.csdnimg.cn/537c5d31161244c0a4287c3f0e1bc78e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
会打开如下界面：![如果是第一次进入，直接点击ok即可](https://img-blog.csdnimg.cn/b6fc887e79a6488ba3a1f2ac9f318fe6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_10,color_FFFFFF,t_70,g_se,x_16)
然后勾选「Always connect to this server」再按下〔OK〕。建议选中“总是连接到本服务器”的选项，即表示每次启动管理控制台，都是管理本机的 Filezilla 服务。

1.首先打开管理控制台，点击左起第四个图标进入系统设置。
![进入系统设置](https://img-blog.csdnimg.cn/aa3023b57d444a6e89023ae9d2f3c709.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
2.打开 ftp 用户管理界面，点击右侧的 add 按钮，添加新用户。 
3.在新增用户的对话框中，输入“anonymous”这个名字，即FTP的匿名用户。 
![添加匿名用户](https://img-blog.csdnimg.cn/77b1c5d15e15464bbe15094817aa0213.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
4.点击确认，添加用户完成，返回用户管理界面。 
5.点击左侧的“Shared folders”菜单。点击Add按钮，添加 d:\web2002 目录。 
6.打开浏览文件夹的选项，选择要设置FTP的目录。 
7.点击确定，添加用户完成。
![添加目录](https://img-blog.csdnimg.cn/d0f5c6c95b884612865d53ea5f1ec12c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![并将其设为home dir](https://img-blog.csdnimg.cn/f4bd8179f75344a1bc12192b1b4deaf7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
![开放相应权限](https://img-blog.csdnimg.cn/a28aa3cbf58a4318aa85f7e6aad8c94c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
现在用户FTP客户端连接到 FileZilla Server上，可以看到匿名 FTP 已经配置完成。 

复制test文件添加进来试试：
![复制test文件添加进来试试](https://img-blog.csdnimg.cn/797aed99b71b4167a7ee4ca81d6a3250.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
打开本地 d:\web2002\ 已存在上传的文件：
![打开本地 d:\web2002\ 已存在上传的文件](https://img-blog.csdnimg.cn/ec2c4ca8369544c6854830ba30dc4359.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
ftp 上传文件成功。
### 比较操作上的区别
www 上传：即通过浏览器来上传文件。

1、通过浏览器上传文件，按照“操作向导”一步步操作完成；
2、支持断点续传，支持大文件上传；

ftp 上传：

1、需要建立 FTP 服务器及配置设置，专业性强；
2、不支持断点续传，只能重新上传，支持大文件上传；

## FileZilla Server 详细配置解析

注意：修改端口和密码非常重要，这是确保 Filezilla 安全的重点，必须修改端口，必须设置密码！密码建议足够复杂！可以在管理界面中进行修改：

首先要进行服务器全局参数设置：

1、General settings（常规设置）：

Listen on Port：监听端口，其实就是FTP服务器的连接端口。（一般都是21）
Max.Number of users：允许最大并发连接客户端的数量。（0为不限制）
Number of Threads：处理线程。也就是CPU优先级别。数值调得越大优先级越高，一般默认即可。

下面的是超时设置，

Connections timeout：连接超时时间；此处默认是120秒。
No Transfer timeout：传输空闲超时；此处默认是120秒。
Login timeout：登入超时。此处是60秒。

FileZilla Server全局参数设置

1.1、Welcome message：页面设置客户端登录成功以后显示的Welcome信息。
![Welcome message](https://img-blog.csdnimg.cn/14e518600f8b49348e5080818f115a7d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
站长此处已经改为Welcom to  FTP Server！此处最好要修改！因为随便暴露的话黑客可能会利用漏洞进行攻击。建议和站长输入的一样即可。 

1.2、IP bindings（IP绑定）页面：把服务器与IP地址绑定，使用*以绑定到所有地址。（一般默认即可）
![IP bindings](https://img-blog.csdnimg.cn/bc8a644ecaf847e7bd6c41c91ea55704.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
1.3、IP Filter（IP过滤器）页面：设置IP过滤规则，在上面栏目中的IP是被禁止与FTP服务器连接的，下面的是允许的。

格式：可以是单个IP地址、IP地址段，可以使用通配符、使用IP/subnet语法或正则表达式（以“/”结尾）来过滤主机名。

（一般默认即可，除非有需要的话再来进行设置）
![IP Filter](https://img-blog.csdnimg.cn/8887308e57e7485aba1e9ad2adb7c665.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
2、Passive mode settings（被动传输模式设置）：这个页面要重点关注。
![Passive mode settings](https://img-blog.csdnimg.cn/11d199659c484cbca8dc9dff30f719fa.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)

先修改Use custom port range：此处根据自己需要选择（例：10000-10020）。

下面是被动传输设置：

 1.如果服务器本身直接拥有公网IP，可以选软件默认的“Default”。

 2.如果服务器是在局域网里面，在一个网关后面，那么就要选择第二项“Use the follwoing IP”，并且在下面的输入栏填写公网的IP地址；否则，客户端用PASV被动模式可能无法连接FTP服务器。因为服务器是在内网中，在客户端使用PASV模式连接服务器的时候，服务器收到连接请求之后需要把自身的IP地址告诉客户端，由于服务器在内网中，它侦测到的IP地址是内网的（如192.168.0.5），它把这个IP地址交给客户端，客户端自然无法连接。在这里设置了指定的IP地址后，服务器就会把这个公网合法的IP地址提交给客户端，这样才能正常建立连接。如果服务器是动态IP的，那么可以选择下面的“Retrieve external IP address from”，利用FileZilla官方网站免费提供的IP查询页面获取当时的公网合法IP，然后服务器把这个公网合法IP地址提交给客户端。当然静态IP也可以用这个，只不过没有必要。

这个设置页面对服务器位于内网的情况非常重要。有些FTP服务器端没有这个设置项目，客户端就只能用Port主动模式连接。当然有些客户端软件针对这个问题有专门的设置，如FlashFXP的站点设置中只要选中“被动模式使用站点IP”就可以了。

对于在局域网中的服务器，如果服务器没有置于DMZ区，那么强烈建议选中下面的“Use custom port range”定义PASV端口范围。由于PASV模式中，是服务器随机打开端口，然后把打开的端口号告诉客户端，让客户端连接打开的端口。但是因为服务器处于网关后面，如果网关那里没有做对应的端口映射，客户端从外网就无法连接服务器打开的端口，导致PASV模式连接失败。在这里限定服务器打开的端口范围，然后到连接外网的网关那里，对服务器的这些端口做端口映射（虚拟服务）。这需要服务器和Internet网关设备配合设置，这样外网的客户端才能用PASV模式连接进来。

3、Security settings（安全设置）：

这里的两个选项关系到能否FXP。软件默认状态“Block incoming server-to-server transfers”和“Block outgoing server-to-server transfers”两项都是选中的，前面那项是禁止连入的服务器对传，后面是禁止传出的服务器对传。也就是说默认状态不允许FXP，如果需要使用FXP，那么就把这两个项目取消选择。注意FXP传输除了跟这个页面的设置有关，还跟IP过滤器有关。

![Security settings](https://img-blog.csdnimg.cn/dc5aeaa565d04aa58723619a1b4ab85e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
4、miscellaneous：杂项设置。
![miscellaneous](https://img-blog.csdnimg.cn/7f4e3942feb240a2813978c63a7bae78.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
默认即可。

5、 Admin Interface setting（管理员界面设定）：

这个就是登录配置服务器界面的一些参数。端口号的设置在安装的时候也出现过。下面两栏可以定义允许远程登录配置的网络界面和IP地址，第一个空白可以设置把管理界面绑定到IP地址，使用*以绑定所有IP地址，127.0.0.1是默认绑定，它一直存在且不可被移除；第二个空白设置允许连接到管理界面的IP地址，可以使用通配符（例如：123.234.12？.*），127.0.0.1总是被允许连接到管理界面的。在最下面更改管理员口令。
![Admin Interface setting](https://img-blog.csdnimg.cn/0021331d8ad8479aafde7036edb0b49b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
注意：修改端口和密码非常重要，这是确保Filezilla安全的重点，必须修改端口，必须设置密码！密码建议足够复杂！

6、Logging（日志）：设定是否启用日志记录功能以及日志文件大小和文件名。
![Logging](https://img-blog.csdnimg.cn/473b6877fdb44169b68116669693c995.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
7、Speed Limits（速度限制）：

这个是全局参数，默认状态不限速。可以选中“Constant Speed Limit of”并填写限速数值来实现速度限制，下载（传出）和上传（传入）可以分别设置。还可以根据时段自定义限速规则——“Use Speed Limit Rules”，比如这台服务器或者网络连接除了做FTP服务器之外还有别的用途，需要根据时间调度，不能让FTP传输挤占所有网络带宽影响其它的网络服务；就可以通过这里设置。

![Speed Limits](https://img-blog.csdnimg.cn/0fac47f4f2e94edcbeca1047705159dc.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
8、Filetransfer compression（文件传输压缩设置）：

MODE Z FTP协议是一种实时压缩的传输协议。在这种模式下，发送方的数据在发出之前先进行压缩，再送到网络链路中传输，接收方将收到数据实时解包，在本地还原重组成原文件。这种模式可以大幅度减少网络中的数据流量，提升传输效率（速度）。当然对于已经压缩过的文件，就几乎没有效果了。要使用这种传输模式，需要服务器端和客户端都支持MODE Z协议。
![Filetransfer compression](https://img-blog.csdnimg.cn/8e98a08cb00146fa9ce3783d36fee802.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
勾选“Enable MODE Z support”就可以启用本服务器的MODE Z支持功能，这样，只要客户端也支持MODE Z就可以获得它带来的性能提升。“Minimum allowed compression level”和“Maximum allowed compression level”分别设置最小压缩率和最大压缩率。最下面可以输入不启用MODE Z功能的目标IP。

9、设置“SSL/TLS settings”：安全套接层协议设置
![SSL/TLS settings](https://img-blog.csdnimg.cn/fc693b29fb1248c59f75c1b9da11c18e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
选中“Enable FTP over SSL/TLS support(FTPS)”进行公钥私钥的设置.

10、Autoban：自动断开
![Autoban](https://img-blog.csdnimg.cn/d014757c42924b3385438251bc4113d0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
FileZilla Server配置勾选是否一小时之内允许重复10次失败尝试。

参考链接：[https://www.5xiaobo.com/?id=528](https://www.5xiaobo.com/?id=528)
