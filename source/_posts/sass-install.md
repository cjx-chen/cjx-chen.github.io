---
title: Sass 基础
date: 2020-08-08 18:52:39
img: https://pic1.zhimg.com/v2-13b0a4f0258c7cb20d93f505852a9a1e_1440w.jpg?source=172ae18b
categories: 
- 安装配置步骤
- 前端
tags:
- Sass
---

## Sass 环境安装和编译
在安装 Sass 之前要先安装 Ruby，因为 Sass 是基于 Ruby 开发的；

首先我们先打开 [Ruby官网](http://www.ruby-lang.org/zh_cn/)，并按照官网的说明以及[菜鸟教程的说明](https://www.runoob.com/ruby/ruby-installation-windows.html)安装 Ruby：
![](https://img-blog.csdnimg.cn/20200805161227505.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
打开 cmd，安装 Sass（需要联网）：
在命令提示符输入 `gem install sass` 回车；
![](https://img-blog.csdnimg.cn/20200805203938339.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
验证 Sass 是否安装成功：
![](https://img-blog.csdnimg.cn/20200805204031628.png)
安装 compass：
在命令提示符输入 `gem install compass` 回车；
![](https://img-blog.csdnimg.cn/20200805204159171.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
验证 Compass 是否安装成功：
![](https://img-blog.csdnimg.cn/20200805204238154.png)
再给 VSCode 安装一个插件就可以了：
![](https://img-blog.csdnimg.cn/20200805204335680.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

## 在 Vue 项目中配置 Sass
### 安装 Sass 依赖包
打开 VSCode，新建一个终端，（使用淘宝镜像）安装相关插件：
```powershell
cnpm install sass  --save-dev
cnpm install node-sass --save-dev
cnpm install sass-loader --save-dev
```
### 添加配置
打开build文件夹下的webpack.base.conf.js，如下图：
![](https://img-blog.csdnimg.cn/20200805204720455.png)
找到module.exports里的module，在rules里添加下面的配置：

```javascript
{
  test: /\.sass$/,
  loaders: ['style', 'css', 'sass']
}
```
如下图所示：
![](https://img-blog.csdnimg.cn/2020080520481940.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
### 修改 style 标签
在vue文件中修改style标签，即可使用sass；
```html
<style lang="scss">
```

## Sass 基础语法
demo1.scss

```ruby
$abc:red;
$efg:yellow;
$color: #e03434;

$width: 300px;
$height: 300px;

$basewidth: 200px;
$basewidth: 100px !default;
// 默认值

.div {
    color: $abc;
    width: 111px;
}

.div1 {
    color: $abc;
    width: 110px;
}

.div2 {
    width: $width;
    height: $height;

    background-color: $color;
}
```
demo1.css

```css
.div {
  color: red;
  width: 111px;
}

.div1 {
  color: red;
  width: 110px;
}

.div2 {
  width: 300px;
  height: 300px;
  background-color: #e03434;
}
```
demo2.scss

```ruby
$width: 300px;
$height: 300px;

$color: #e03434;

$str: 'hello.jpeg';
$strNoQout: abc; 
$class: '.div';
$styleKey: 'idth';

.div1 {
    width: $width;
    height: $height;

    background-color: $color;

    background-image: url('./img/' + $str);
    background-image: url('./img/' + $strNoQout);
    background-image: url('./img/#{$strNoQout}');
}

#{$class} {
    width: $width;
    height: $height;
}

#{$class} {
    w#{$styleKey}: $width;
}
```
demo2.css

```css
.div1 {
  width: 300px;
  height: 300px;
  background-color: #e03434;
  background-image: url("./img/hello.jpeg");
  background-image: url("./img/abc");
  background-image: url("./img/abc");
}

.div {
  width: 300px;
  height: 300px;
}

.div {
  width: 300px;
}
```
demo3.scss

```ruby
$width: 300px;
$color: #ffe932;

.div1 {
    width: $width;
    height: $width;

    $widthInner: 100px;
    width: $widthInner;
}
```
demo3.css

```css
.div1 {
  width: 300px;
  height: 300px;
  width: 100px;
}
```
demo4.scss

```ruby
// @import 'org.css';
@import '_base.scss';
$width: 300px;
$color: #ffe932;

.div {
    width: 300px;
}
```
_base.scss

```ruby
body {
    margin: 0;
    padding: 0;
}
```
demo4.css

```css
body {
  margin: 0;
  padding: 0;
}

.div {
  width: 300px;
}
```

## Sass 常见的基本数据类型
### 数字类型

```ruby
$width: 300px;
$zoomValue: 2;

// number
.div {
    width: $width;
    height: $width;
    zoom: $zoomValue;
}
```

### 颜色类型

```ruby
$color: red;
$colorHex: #ffe932;

// color
.div {
    color: $color;
    background-color: $colorHex;
}
```

### 字符串类型

```ruby
$str: 'hello.jpeg';

// string
.div {
    background-image: url('images/' + $str);
}
```

### 数组类型

```ruby
$list: (100px,200px,'string',2);
// Sass 数组的下标是从1开始的

// list
.div {
    width: nth($list, 1);
    height: nth($list, 2);

    zoom: index($list, 'string');
}
```

### map类型

```ruby
$map: (top: 1px, left: 2px, bottom: 3px, right: 4px);

// map
.div {
    top: map-get($map, top);
    left: map-get($map, left);
}
.div {
    @each $key, $value in $map {
        #{$key}: $value;
    }
}
```
### demo.css

```css
.div {
  width: 300px;
  height: 300px;
  zoom: 2;
}

.div {
  color: red;
  background-color: #ffe932;
}

.div {
  background-image: url("images/hello.jpeg");
}

.div {
  width: 100px;
  height: 200px;
  zoom: 3;
}

.div {
  top: 1px;
  left: 2px;
}

.div {
  top: 1px;
  left: 2px;
  bottom: 3px;
  right: 4px;
}
```

## Sass 加减乘除基本运算
demo.scss

```ruby
$num1: 100px;
$num2: 200px;

$width: $num1 + $num2;

$color1: #010203;
$color2:#040506;
$color3: #a69e61;

$str: 'hello.jpeg';

.div {
    width: $width;
}

// 加减乘除
.div {
    font: 10px/8px;     //wrong
    font: (10px/8);
    font: (10px*8);
    font: $width/2;
    margin-left: (5px + 8px/2);;
}

// 颜色运算
.div {
    color: $color1 + $color2;   //wrong
    // 混合两种颜色
    color: mix($color1, $color2); 
    // 获取rbg
    color: red($color1);
    color: green($color1);
    color: blue($color1);

    color: rgb(red($color3), green($color3), blue($color3));
}

// 字符串
.div {
    background-image: url('images/' + $str);
}
```
demo.css

```css
.div {
  width: 300px;
}

.div {
  font: 10px/8px;
  font: 1.25px;
  font: 80px;
  font: 150px;
  margin-left: 9px;
}

.div {
  color: #050709;
  color: #030405;
  color: 1;
  color: 2;
  color: 3;
  color: #a69e61;
}

.div {
  background-image: url("images/hello.jpeg");
}
```

## Mixin（混合宏）用法
demo.scss

```ruby
// 一般mixin
@mixin helloMixin {
    display: inline-block;

    font: {
        size: 20px;
        weight: 500;
    };

    color: red;
}

// 嵌套mixin
@mixin helloMixin2 {
    padding: 10px;

    @include helloMixin;

    background-color: red;
}

// 参数mixin
@mixin sexy-border($color, $width) {
    border: {
        color: $color;
        width: $width;
        style: dashed;
    };
}

.div {
    width: 100px;
    @include helloMixin2;
}

.div {
    @include sexy-border(blue, 2px);
}
```
demo.css

```css
.div {
  width: 100px;
  padding: 10px;
  display: inline-block;
  font-size: 20px;
  font-weight: 500;
  color: red;
  background-color: red;
}

.div {
  border-color: blue;
  border-width: 2px;
  border-style: dashed;
}
```

## Sass 继承和嵌套
### 嵌套
demo.scss

```ruby
$width: 300px;
$color: #fff;

.div1 {
    width: $width;
    height: $width;
    background-color: $color;

    .div-inner {
        width: $width;
        height: $width;
        background-color: $color;
        .div-inner-inner {
            width: $width;
            height: $width;
            background-color: $color;
        }
    }

    a {
        color: red;
    }
}

.div1{
    width: $width;
    height: $width;
    background-color: $color;

    .div-inner {
        border: {
            left: 1px solid #000;
            top: 2px solid #000;
        };
        background: {
            image: url('abc.png');
            color: #000;
        };
    }
}
```
demo.css

```css
.div1 {
  width: 300px;
  height: 300px;
  background-color: #fff;
}

.div1 .div-inner {
  width: 300px;
  height: 300px;
  background-color: #fff;
}

.div1 .div-inner .div-inner-inner {
  width: 300px;
  height: 300px;
  background-color: #fff;
}

.div1 a {
  color: red;
}

.div1 {
  width: 300px;
  height: 300px;
  background-color: #fff;
}

.div1 .div-inner {
  border-left: 1px solid #000;
  border-top: 2px solid #000;
  background-image: url("abc.png");
  background-color: #000;
}
```

### 继承
#### 简单继承
demo.scss
```ruby
// 简单继承
.div {
    border: 1px;
    background-color: red;
}

.divext {
    @extend .div;
    border-width: 3px;
}
```
#### 关联属性继承
demo.scss

```ruby
// 关联属性继承
.div1 {
    border: 1px;
    background-color: red;
}

.div1.other {
    background-image: url('hello.jpeg');
}

.divext {
    @extend .div1;
}
```
#### 链式继承
demo.scss
```ruby
// 链式继承
.div1 {
    border: 1px solid #000;
}

.div2 {
    @extend .div1;
    color: red;
}

.div3 {
    @extend .div2;
    color: #000;
}
```

#### 伪类继承
demo.scss
```ruby
// 伪类继承
a:hover {
    text-decoration: underline;
}

:hoverlink {
    color: red;
    @extend :hover
}
```
#### demo.css
```css
.div, .divext {
  border: 1px;
  background-color: red;
}

.divext {
  border-width: 3px;
}

.div1, .divext, .div2, .div3 {
  border: 1px;
  background-color: red;
}

.div1.other, .other.divext, .other.div2, .other.div3 {
  background-image: url("hello.jpeg");
}

.div1, .divext, .div2, .div3 {
  border: 1px solid #000;
}

.div2, .div3 {
  color: red;
}

.div3 {
  color: #000;
}

a:hover, a:hoverlink {
  text-decoration: underline;
}

:hoverlink {
  color: red;
}
```

## Sass 条件控制
@if，@for，@while，@each 等条件控制语句；

### @if
demo.scss

```ruby
// if

$type: 'tony';

p {
    @if $type == 'bufy' {
        color: red;
    } @else if $type == 'tim' {
        color: blue;
    } @else if $type == 'tony' {
        color: green;
    } @else {
        color: black;
    }
}

@if $type == 'bufy' {
    .div {
        color: red;
    }
} @else {
    .div {
        color: blue;
    }
}
```
### @for
demo.scss

```ruby
// for
@for $i from 1 through 3 {      //through包括3
    .item#{$i} {
        width: 1px * $i;
    }
}

@for $i from 1 to 3 {       //to不包括3
    .item#{$i} {
        width: 1px * $i;
    }
}

// for list
$list: (1,2,3,4,5);

@for $i from 1 through length($list) {
    .item#{$i} {
        width: 1px * $i;
    }
}
```
### @while
demo.scss

```ruby
// while
$i: 6;

@while $i > 0 {
    .item#{$i} {
        width: 1px * $i;
    }

    $i: $i - 2;
}
```
### @each
demo.scss

```ruby
// each
$map: (top: 1px, left: 2px, bottom: 3px, right: 4px);

.div {
    @each $key, $value in $map {
        #{$key}: $value;
    }
}
```
### demo.css

```css
p {
  color: green;
}

.div {
  color: blue;
}

.item1 {
  width: 1px;
}

.item2 {
  width: 2px;
}

.item3 {
  width: 3px;
}

.item1 {
  width: 1px;
}

.item2 {
  width: 2px;
}

.item1 {
  width: 1px;
}

.item2 {
  width: 2px;
}

.item3 {
  width: 3px;
}

.item4 {
  width: 4px;
}

.item5 {
  width: 5px;
}

.item6 {
  width: 6px;
}

.item4 {
  width: 4px;
}

.item2 {
  width: 2px;
}

.div {
  top: 1px;
  left: 2px;
  bottom: 3px;
  right: 4px;
}
```

## Sass 函数
### 内置函数
#### 字符串函数

 - unquote($string)：去除引号；
 - quote($string)：添加引号；
 - str-length($string)：获取字符串长度；
 - str-insert($string, $insert, $index)：在指定位置插入字符；
 - str-index($string, $substring)：返回指定字符在字符串的位置；
 - to-upper-case($string)：转换成大写；
 - to-lower-case($string)：转换成小写；

demo.scss

```ruby
// string
$string: 'hello';
$stringNo: hello;

$stringUP: 'HELLO';

.div {
    background-image: unquote($string);

    background-image: quote($stringNo);

    background-image: str-length($string);

    @debug str-insert($string, 'p', 2);

    @debug str-index($string, $substring: "l");

    background-image: to-upper-case($string);

    background-image: to-lower-case($stringUP);
}
```
demo.css

```css
.div {
  background-image: hello;
  background-image: "hello";
  background-image: 5;
  background-image: "HELLO";
  background-image: "hello";
}
```

#### 数字函数

 - percentage($number)：转换成百分比；
 - round($number)：执行标准舍入，即它总是将数值四舍五入为最接近的整数；
 - ceil($number)：执行向上舍入，即它总是将数值向上舍入为最接近的整数；
 - floor($number)：执行向下舍入，即它总是将数值向下舍入为最接近的整数；
 - abs($number)：获取绝对值；
 - min($number)：获取最小值；
 - max($number)：获取最大值；
 - random()：获得随机数；

demo.scss
```ruby
$number: 70;
$number2: 71;

$numberPercent: 0.77;

$numberRound: 25.9;

$abs: -3;

.div {
    zoom: percentage($numberPercent);

    zoom: round($numberRound);

    zoom: ceil($numberRound);

    zoom: percentage($numberRound);

    zoom: abs($abs);

    zoom: min($number, $number2);

    zoom: max($number, $number2);

    zoom: random(10);       //在0到10之间取随机整数

    zoom: random();     //在0到1之间取随机数
}
```
demo.css

```css
.div {
  zoom: 77%;
  zoom: 26;
  zoom: 26;
  zoom: 2590%;
  zoom: 3;
  zoom: 70;
  zoom: 71;
  zoom: 10;
  zoom: 0.60628;
}
```
#### 数组函数

 - length($list)：获取数组长度；
 - nth($list, $n)：获取指定下标的元素，下标从 1 开始；
 - set-nth($list, $n, $value)：替换指定下标的元素；
 - join($list1, $list2)：拼接数组；
 - append($list1, $val, [ $sesparator])：从数组尾部添加元素；
 - index($list, $value)：返回指定元素在数组中的位置；

demo.scss

```ruby
// list
$list: (1,'p',3,4,5);

.div {
    zoom: length($list);
    zoom: nth($list, 2);

    //不懂
    @debug set-nth($list, 1, 'x');      
    @debug join($list, (6,7,8));
    @debug append($list, '999');
    @debug index($list, 'p');
}
```
demo.css

```css
.div {
  zoom: 5;
  zoom: "p";
}
```
#### map 函数

 - map-get($map, $key)：根据给定的 key 值，返回 map 中相关的值；
 - map-merge($map1, $map2)：将两个 map 合并成一个新的 map；
 - map-remove($map, $key)：从 map 中删除一个 key，返回一个新 map；
 - map-keys($map)：返回 map 中所有的 key；
 - map-values($map)：返回 map 中所有的 value；
 - map-has-key($map, $key)：根据给定的 key 值判断 map 是否有对应的 value 值，如果有返回 true，否则返回 false；
 - keywords($args)：返回一个函数的参数，这个参数可以动态的设置 key 和 value；

demo.scss

```ruby
// map
$map: (top: 1px, left: 2px, bottom: 3px, right: 4px);

.div {
    width: map-get($map, top);
    @debug map-remove($map, bottom);
    @debug map-keys($map);
    @debug map-values($map);
    @debug map-has-key($map, abc);
}

@mixin foo($args...) {
    @debug keywords($args);
}

@include foo($arg1:'abc', $arg2:'efg');
```
demo.css

```css
.div {
  width: 1px;
}
```

### 自定义函数
demo.scss

```ruby
// 自定义函数
$rem1: 100px;

@function px2rem($px) {
    $rem: 37.5px;

    @debug $px;

    @return ($px/$rem) + rem;
};

.div {
    width: px2rem($rem1);
}
```
demo.css

```css
.div {
  width: 2.66667rem;
}
```

## Sass 页面实战
### 环境准备
详情看前面；
### 页面样式 html 编写
整个项目大约需要这些文件：
![](https://img-blog.csdnimg.cn/2020080818483314.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
下面大家参照源码自己试试吧：

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scaleble=0">
    <link rel="stylesheet" type="text/css" href="index.css">
    <title>今日头条</title>
</head>
<body>
    <div class="header">
        <div class="title_logo"></div>
    </div>
    <div class="top_bar">
        <div class="top_menu_list">
            <a class="btn cur">推荐</a>
            <a class="btn">视频</a>
            <a class="btn">热点</a>
            <a class="btn">社会</a>
            <a class="btn">娱乐</a>
            <a class="btn">军事</a>
            <a class="btn">科技</a>
            <a class="btn">汽车</a>
            <a class="btn">体育</a>
            <a class="btn">财经</a>
            <a class="btn">国际</a>
            <a class="btn">时尚</a>
        </div>
    </div>
    <div class="content_list">
        <section class="section_item">
            <div class="item_detail">
                <h3 class="title">一图读懂 | 秀突然单人四排释放哪些重大信号？</h3>
                <div class="item_info">
                    <span class="stick_label">置顶</span>
                    <span class="src">新华社</span>
                    <span class="cmt">评论 2473</span>
                    <span class="time">2分钟前</span>
                </div>
            </div>
        </section>
        <section class="images_item">
            <div class="item_detail">
                <h3 class="title">震惊！嘻嘻帮绵绵冰上分途中竟狂掉200分？</h3>
                <div class="list_image">
                    <ul>
                        <li class="list_img_holder"><img src="./assets/img1.jpg"></li>
                        <li class="list_img_holder"><img src="./assets/img2.jpg"></li>
                        <li class="list_img_holder"><img src="./assets/img3.jpg"></li>
                    </ul>
                </div>
                <div class="item_info">
                    <span class="hot_label">热</span>
                    <span class="src">青蜂侠</span>
                    <span class="cmt">评论 7028</span>
                    <span class="time">1分钟前</span>
                </div>
            </div>
        </section>
        <section class="images_item">
            <div class="item_detail">
                <h3 class="title">重大消息！钢强王10日假期将尽，原因竟是...</h3>
                <div class="list_image">
                    <ul>
                        <li class="list_img_holder"><img src="./assets/img1.jpg"></li>
                        <li class="list_img_holder"><img src="./assets/img2.jpg"></li>
                        <li class="list_img_holder"><img src="./assets/img3.jpg"></li>
                    </ul>
                </div>
                <div class="item_info">
                    <span class="hot_label">热</span>
                    <span class="src">青蜂侠</span>
                    <span class="cmt">评论 7028</span>
                    <span class="time">1分钟前</span>
                </div>
            </div>
        </section>
        <section class="image_item">
            <div class="item_detail">
                <h3 class="title"> 沙漠小卖部嗨翻全场，可乐每满99减50，走过路过不要错过！</h3>
                <div class="one_image">
                    <img src="./assets/img3.jpg">
                </div>
                <div class="item_info">
                    <span class="gg_label">广告</span>
                    <span class="src">京东</span>
                    <span class="cmt">评论</span>
                    <span class="time">1分钟前</span>
                </div>
            </div>
        </section>
    </div>
</body>
</html>
```
图片文件大家可以随意按照自己喜欢的去添加；

### Sass编写和编译
首先我们需要一个情况所有固有样式的 CSS 文件，因而创建一个 reset.scss，其源码为：

```ruby
html,
body,
div,
span,
object,
button,
iframe,
h1,
h2,
h3,
h4,
h5,
h6,
p,
blockquote,
a,
code,
em,
img,
q,
small,
strong,
dd,
dl,
dt,
li,
ol,
ul,
fieldset,
form,
label,
table,
tbody,
tr,
th,
td,
input {
    margin: 0;
    padding: 0;
    border: 0;
}
body {
    position: relative;
    width: 100%;
    overflow: hidden;
}
ul,
li {
    list-style-type: none;
}
a {
    text-decoration: none;
}
// @charset "utf-8";
html {
    background: #fff;
    font-family: 'STHeiti', 'Microsoft YaHei', 'Helvetica', 'Arial';
    -webkit-text-size-adjust: none;
    word-break: break-word;
}
```

然后是 html 基本样式的 index.scss：

```ruby
@import './reset.scss';

$baseFontSize: 17px;
$redColor: #d43d3d;
$blueColor: #2a90d7;
$assetsDir: 'assets';

@mixin sectionStyle {
    margin-left: 15px;
    margin-right: 15px;

    border-bottom: 1px solid rgba(211, 211, 211, 0.6);

    padding-top: 10px;
    padding-bottom: 10px;
}

@mixin hotLabel($color) {
    font-size: 14px;
    color: $color;

    border: 1px solid $color;
}

@mixin line2 {
    overflow: hidden;
    text-overflow: ellipsis;    //当文字超出就用省略号的方式
    display: -webkit-box;
    display: box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
}

@mixin clearfix {
    // & 是其父元素的意思
    &:after {
        visibility: hidden;
        display: block;
        content: " ";
        clear: both;
        height: 0;
    }
}

@mixin commonImg {
    border: none;
    width: 100%;
    display: block;
}

.header {
    height: 45px;
    background-color: $redColor;
    .title_logo {
        width: 100px;
        height: 100%;
        margin: 0 auto;
        background: {
            position: center;
            size: contain;
            repeat: no-repeat;
            image: url($assetsDir + '/title.png');
        };
    }
}

.top_bar {
    background-color: #f4f5f6;
    height: 34px;
    overflow-x: auto;
    overflow-y: hidden;
    .top_menu_list {
        white-space: nowrap;    //不换行
        overflow: hidden;
        height: 100%;
        display: inline-block;
    }
    .btn {
        padding: 8px;
        display: inline-block;
        font-size: $baseFontSize;
        &.cur {
            color: $redColor;
        }
    }
}

.content_list {
    .section_item {
        @include sectionStyle;
        .title {
            font-size: 20px;
        }
        .item_info_base {
            color: #999;
            font-size: 14px;
        }
        .item_info {
            margin-top: 11px;
            @extend .item_info_base;
        }
        .stick_label {
            @include hotLabel($redColor);   
        }
        .src {
            @extend .item_info_base;
        }
    }
    
    .images_item {
        @extend .section_item;
        .title {
            @include line2;
        }
        .list_image {
            margin-top: 10px;
        }
        .list_img_holder {
            float: left;
            width: 32%;
            height: 50px;
            margin-right: 3px;
            img {
                @include commonImg;
            }
        }
        ul {
            @include clearfix;
        }
        .hot_label {
            @include hotLabel($redColor);   
        }
    }

    .image_item {
        @extend .section_item;
        .one_image {
            height: 160px;
            margin-top: 10px;
            img {
                @include commonImg;
            }
        }
        .gg_label {
            @include hotLabel($blueColor);
        }
    }
}
```
.css 文件会自动生成的，这里就不展示了；

最后，生成的页面如下图所示：
![](https://img-blog.csdnimg.cn/20200808185213529.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
就这样啦，掰掰；

