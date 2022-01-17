---
title: 【Vue3】Vue3.x中的事件和方法全解
date:  2022-01-17 13:55:57
img: https://pic2.zhimg.com/v2-b7df35f5df14059bbcce379a7d2bc494_1440w.jpg?source=172ae18b
categories: 
- Vue3
tags:
- Vue3
- Html
- Javascript
---

## 一、Vue事件方法的简单使用

```html
// template模版
<template>
    <div>
        <h2>{{ msg }}</h2>
        <button @click="setMsg()">改变msg</button>
        <button @click="getMsg()">获取msg</button>
    </div>
</template>
// 业务逻辑
<script>
    export default {
        data() {
            return {
                msg: "你好,Vue!"
            }
        },
        methods: {
            setMsg() {
                this.msg = "改变后的msg";
            },
            getMsg() {
                alert(this.msg);
            }
        }
    }
</script>
```
## 二、v-bind绑定Class
当v-bind与class一起使用时，vue提供了特殊的增强功能style，除了字符串外，表达式还可以求值为对象或者数组

### v-bind: class 绑定字符串

```html
<template>
    <div :class="myClass"></div>
    <button @click="changClass()">改变div颜色</button>
</template>

<script>
    export default {
        data() {
            return {
                myClass: "red",
            }
        },
        methods: {
            changClass() {
                this.myClass = "blue";
            }
        }
    }
</script>

<style scoped="scoped">
    .red {
        width: 200px;
        height: 200px;
        background-color: red;
    }

    .blue {
        width: 200px;
        height: 200px;
        background-color: skyblue;
    }
</style>
```
### v-bind:class 绑定对象

```html
<template>
    <h2>class绑定多个动态属性：对象方式</h2>
    <div :class="{'blue':isActive,'active':isErro}"></div> <!-- 注意：外边双引号，里边单引号 -->
</template>

<script>
    export default {
        data() {
            return {
                isActive: true,
                isErro: false
            }
        },
        methods: {
            changClass() {
                this.myClass = "blue";
            }
        }
    }
</script>

<style scoped="scoped">
    .red {
        width: 200px;
        height: 200px;
        background-color: red;
    }

    .blue {
        width: 200px;
        height: 200px;
        background-color: skyblue;
    }
</style>
```
![](https://img-blog.csdnimg.cn/8a8965d702564acaaafb10a1fa51793f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
### v-bind:class 绑定数组

```html
<template>
    <h2>class绑定多个动态属性：数组方式</h2>
    <div :class="[activeClass,redClass]">前端工程师</div> <!-- 注意：外边双引号，里边单引号 -->
</template>

<script>
    export default {
        data() {
            return {
                redClass: "red",
                activeClass: "active"
            }
        },
        methods: {
            changClass() {
                this.myClass = "blue";
            }
        }
    }
</script>

<style scoped="scoped">
    .red {
        width: 200px;
        height: 200px;
        background-color: red;
    }

    .blue {
        width: 200px;
        height: 200px;
        background-color: skyblue;
    }

    .active {
        line-height: 200px;
        text-align: center;
        font-size: 30px;
        font-weight: bolder;
        color: #fff;
    }
</style>
```
![](https://img-blog.csdnimg.cn/ac26bfb3613a4531a941f429d5881f3d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
### v-bind:class 数组语法：结合三目运算

```html
<template>
    <h2>class绑定多个动态属性：三目运算方式</h2>
    <div class="active" :class="flag?redClass:blackClass">前端工程师</div> <!-- 注意：外边双引号，里边单引号 -->
</template>

<script>
    export default {
        data() {
            return {
                flag: false,
                redClass: "red",
                blackClass: "black",
                activeClass: "active",
            }
        },
        methods: {}
    }
</script>

<style scoped="scoped">
    .red {
        width: 200px;
        height: 200px;
        background-color: red;
    }

    .black {
        width: 200px;
        height: 200px;
        background-color: black;
    }

    .active {
        line-height: 200px;
        text-align: center;
        font-size: 30px;
        font-weight: bolder;
        color: #fff;
    }
</style>
```
![](https://img-blog.csdnimg.cn/ae2100542c8c4c0a8f287205efd767cb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
##  三、v-bind绑定Style
### v-bind绑定style:对象方式
```html
<template>
    <h1 :style="styleObj1">v-bind绑定style:对象方式</h1>
</template>

<script>
    export default {
        data() {
            return {
                styleObj1: {
                    color: "red",
                    "font-weight": "200"
                }
            }
        },
        methods: {}
    }
</script>

<style scoped="scoped">
</style>
```
### v-bind绑定style:数组方式
```html
<template>
    <h1 :style="[styleObj1,styleObj2]">v-bind绑定style:数组方式</h1>
</template>

<script>
    export default {
        data() {
            return {
                styleObj1: {
                    color: "red",
                    "font-weight": "200"
                },
                styleObj2: {
                    color: "green",
                    "font-style": "italic"
                }
            }
        },
        methods: {}
    }
</script>
```
案例：循环数据 第一个数据高亮显示

```html
<template>
    <ul>
        <!-- 循环数据，第一个数据高亮显示 -->
        <li v-for="(item,index) in list" :key="index" :class="{'red':index==0,'blue':index==1}">{{ item }}</li>
    </ul>
</template>

<script>
    export default {
        data() {
            return {
                list: ['腾讯', '阿里巴巴', '百度', '美团'],
            }
        },
        methods: {}
    }
</script>

<style scoped="scoped">
    .red {
        color: red;
    }

    .blue {
        color: blue;
    }
</style>
```
![](https://img-blog.csdnimg.cn/41c7f5a12bf74150b3e641243a4d17d9.png)
## 四、事件方法应用
### 传参

```html
<template>
    <h2>{{ title }}</h2>
    <button @click="setTitle('我是新的值111')">设置title的值1</button>
    <button @click="setTitle('我是新的值222')">设置title的值2</button>
</template>

<script>
    export default {
        data() {
            return {
                title: "我是一个标题"
            }
        },
        methods: {
            setTitle(data) {
                this.title = data;
            },
        }
    }
</script>

<style scoped="scoped">
</style>
```
### 在一个方法中调用另一个方法

```html
<template>
    <h2>{{ msg }}</h2>
    <button @click="setMsg()">设置msg</button>
    <button @click="getMsg()">获取msg</button>
    <button @click="run()">方法中调用方法改变msg的值</button>
</template>

<script>
    export default {
        data() {
            return {
                msg: "你好,Vue!"
            }
        },
        methods: {
            setMsg() {
                this.msg = "我是改变后的msg";
            },
            getMsg() {
                alert(this.msg);
            },
            run() { // 在一个方法中调用另一个方法,通过this调用
                this.getMsg();
            },
        }
    }
</script>

<style scoped="scoped">
</style>
```
## 五、事件对象
有时候我们还需要在内联语句处理程序中访问原始DOM事件，可以使用特殊`$event`变量将其传递给方法；

### 单个参数

```html
// temolate 模版<template>
    <button data-aid="123" @click="eventFn($event)">事件对象</button> <!-- 注意这里$event规范(固定)写法 -->
</template>
// 业务逻辑
<script>
    export default {
        data() {},
        methods: {
            eventFn(e) { // 传入事件对象
                console.log(e);
                e.srcElement.style.background = "yellowgreen"; // srcElement 或者 target都可以获取事件源对象
                console.log(e.srcElement.dataset.aid); // 通过事件对象获取 aid 属性值
                // e.preventDefault(); // 阻止冒泡
                // e.stopPropagation(); // 阻止默认行为
            },
        }
    }
</script>
<style scoped="scoped"></style>
```
### 多个参数

```html
<template>
    <button @click="warn('传入的参数',$event)">多个参数加事件对象</button>
</template>

<script>
    export default {
        data() {},
        methods: {
            warn(message, e) { // 多个参数
                console.log(e);
                if (e) {
                    e.preventDefault();
                }
                alert(message);
            },
        }
    }
</script>

<style scoped="scoped"></style>
```
## 六、多事件处理程序
你可以在事件处理程序中，使用逗号分隔多个事件处理程序（点击一次，执行多个方法）

```html
<template>
    <button @click="one($event),two($event),getMsg()">点击按钮一次执行多个方法</button>
</template>

<script>
    export default {
        data() {
            return {
                msg: "hello vue!",
            }
        },
        methods: {
            getMsg() {
                alert(this.msg);
            },
            one(e) {
                console.log(e);
            },
            two(e) {
                console.log(e);
            }
        }
    }
</script>

<style scoped="scoped"></style>
```
## 七、事件修饰符
vue中阻止冒泡阻止默认行为，可以通过事件对象`event.preventDefault()`,或`event.stopPropagation()`实现，还可以通过事件修饰符实现
### .stop  阻止冒泡

```html
<template>
    <div @click="divHandler">
        <!-- .stop 阻止冒泡 -->
        <input type="button" @click.stop="btnHandler" value="点击按钮">
    </div>
</template>

<script>
    export default {
        data() {},
        methods: {
            divHandler() {
                console.log("父元素");
            },
            btnHandler() {
                console.log("子元素");
            },
        }
    }
</script>

<style scoped="scoped"></style>
```
### .prevent  阻止默认事件(跳转)

```html
<template>
    <a href="https://www.baidu.com" @click.prevent="linkClick">百度</a>
</template>
```
### .capture  添加事件倾听器时使用事件捕获机制（由外向里）

```html
<template>
    <div class="inner" @click.capture="divHandler">
        <input type="button" value="点击按钮" @click.stop="btnHandler" />
    </div>
</template>
```
### .self  只当事件在该元素本身（比如不是子元素）触发时触发回调

```html
<template>
    <div class="inner" @click="divHandler">
        <input type="button" value="点击按钮" @click.stop="btnHandler" />
    </div>
</template>
```
### .once  事件只触发一次

```html
<template>
    <a href="https://www.baidu.com" @click.prevent.once="linkClick">百度</a>
</template>
```

> **.stop 和 .self 的区别:**
.self 只会阻止自己身上冒泡行为的触发，并不会真正阻止冒泡的行为；

## 八、按键修饰符

`.enter`、`.tab`、`.delete` (同时捕获删除或退格键)、`.esc`、`.space`、`.up`、`.down`、`.left`、`.right`

监听键盘事件时，我们通常要检查特定的键，Vue 允许在监听关键事件时`v-on`或`@`在监听关键事件时添加按键修饰符；

```html
<template>
    <input @keyup.enter="sumbit()" type="text">
</template>

<script>
    export default {
        data() {},
        methods: {
            sumbit() {
                alert("提交成功");
            }
        }
    }
</script>

<style scoped="scoped"></style>
```
![](https://img-blog.csdnimg.cn/b977607c285a4d6dbd942bd43e754af3.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Zi75Zi755qE5aaZ5aaZ5bGL,size_20,color_FFFFFF,t_70,g_se,x_16)
