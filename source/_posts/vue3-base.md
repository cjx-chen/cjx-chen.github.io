---
title: Vue3 入门基础（一）
date: 2021-08-02 02:07:50
img: https://img-blog.csdnimg.cn/img_convert/de2eb89454a66222dcaf49f5848167d5.png
categories: 
- 安装配置步骤
- Vue3
tags:
- Vue3
---

## 创建项目

在项目目录下打开终端，输入：
```vue create <项目名>```

选择 Vue 3：
![](https://img-blog.csdnimg.cn/36c10638ca614a319e330f9721cc70cb.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

项目自动创建好之后，根据提示的命令运行项目：
![](https://img-blog.csdnimg.cn/cf5d4fd18acc46caa47f6cb1127cd300.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)

运行完成后 Ctrl + 单击链接打开运行项目：
![](https://img-blog.csdnimg.cn/bf6f737a17da447ba3a6c4db52cd1fc5.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
网页界面如下：
![](https://img-blog.csdnimg.cn/3c704219879b421e9377db49044ade71.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0plc3NpZWVlZWVlZQ==,size_16,color_FFFFFF,t_70)
## 模板语法
### 插值
#### 文本
数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

```html
<template>
  <span>Message: {{ msg }}</span>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      msg: '我是插值-文本'
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

Mustache 标签将会被替代为对应组件实例中 `msg` property 的值。无论何时，绑定的组件实例上 msg property 发生了改变，插值处的内容都会更新。

#### 原始 HTML
双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用 `v-html` 指令：

```html
<template>
  <p>Using v-html directive: <span v-html="rawHtml"></span></p>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      rawHtml: '<span style="color: red">我是插值-原始HTML</span>'
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

这个 span 的内容将会被替换成为 property 值 `rawHtml`，直接作为 HTML——会忽略解析 property 值中的数据绑定。

注意，你不能使用 v-html 来复合局部模板，因为 Vue 不是基于字符串的模板引擎。反之，对于用户界面 (UI)，组件更适合作为可重用和可组合的基本单位。

> TIP：在你的站点上动态渲染任意的 HTML 是非常危险的，因为它很容易导致 XSS 攻击。请只对可信内容使用 HTML 插值，绝不要将用户提供的内容作为插值。

#### Attribute
Mustache 语法不能在 HTML attribute 中使用 ，然而，可以使用 v-bind 指令：

```html
<template>
  <button v-bind:disabled="isButtonDisabled">我是插值-Attribute按钮</button>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isButtonDisabled: null
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

如果 `isButtonDisabled` 的值是 `null` 或 `undefined`，则 `disabled` attribute 甚至不会被包含在渲染出来的 `<button>` 元素中。

注意：可以把 `isButtonDisabled` 的值改为 `null` 或 `undefined` 或 `false` 或 `true` 看看变化；

---
##### attribute 和 property 的概念
attribute 和 property 是 Web 开发中，比较容易混淆的概念。

简单的说，attribute 是元素标签的属性，property 是元素对象的属性，例如：

```html
<input id="input" value="test value">
<script>
let input = document.getElementById('input');
console.log(input.getAttribute('value')); // test value
console.log(input.value); // test value
</script>
```

- input 的 `value` attribute 是通过标签里的 `value=“test value”` 定义的，可以通过`input.getAttribute(‘value’)` 获取，可以通过 `input.setAttribute(‘value’, ‘New Value’)` 更新
- input 的 `value` property 可通过 `input.value` 获取和更新，初始值是与 attribute 中的赋值一致的。

---
##### attribute 和 property 的绑定
如果在最开始的时候，更新 attribute value 的值，property 的值也会随之改变。

但是更新 property value 的值（在文本框输入或给 input.value 赋新值 ），attribute 的值不会随之改变，而且此时再更新 attribute 的值，property 的值也不再随之改变。

这其实是脏值标记（dirty value flag）在起作用，dirty value flag 的初始值为 `false`，即 attribute value 的更新默认会改变对应的 property value，但是一旦用户交互修改了 property value，dirty value flag 的值就变为 `true`，即 attribute value 的更新就不会改变对应的 property value 了。

所以在实际项目中，我们一般都是在处理作为 property 的 value；

---
##### Vue.js 对 value 的处理
**一般情况使用 `:value`**
Vue.js 的 `v-bind`，一般情况下是在处理 attribute，如果要作为 property 处理的话，需要加上 `.prop`。

不过，`v-bind:value` 却大都默认为处理 property 值，因为被强制转化了，例如：

```html
<input id="input" :value="'test value'" >
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
let input = new Vue({
  el: '#input',
  mounted () {
    console.log(this.$el.getAttribute('value')); // null
    console.log(this.$el.value); // test value
    console.log(this._vnode.data) // {attrs: {id: "input"}, domProps: {value: "test value"}}
  }
});
</script>
```

可见，Vue.js 将 `value` 作为 VNode 的 `data` 中的 `domProps` 的属性，而不是 `attrs` 的属性，所以挂载后会成为作为 property 的 `value`。

在 Vue.js 源码中，强制转化 property 的处理如下：

```html
// src/compiler/parser/index.js
function processAttrs (el) {
...
        if ((modifiers && modifiers.prop) || (
          !el.component && platformMustUseProp(el.tag, el.attrsMap.type, name)
        )) {
          addProp(el, name, value, list[i], isDynamic)
        } else {
          addAttr(el, name, value, list[i], isDynamic)
        }
```
其中 platformMustUseProp 在 web 平台的定义如下：

```html
// src/platforms/web/util/attrs.js
const acceptValue = makeMap('input,textarea,option,select,progress')
export const mustUseProp = (tag: string, type: ?string, attr: string): boolean => {
  return (
    (attr === 'value' && acceptValue(tag)) && type !== 'button' ||
    (attr === 'selected' && tag === 'option') ||
    (attr === 'checked' && tag === 'input') ||
    (attr === 'muted' && tag === 'video')
  )
}
```
由上可知，类型不为 button 的 input，textarea，option，select，progress 的 `value` 会强制作为 property，而不需要设置为 `:value.prop`。

例如 textarea 标签，其本身其实并不支持 value attribute，所以以下代码中的 `value` 的值并不会显示在多行文本框中：

```html
<textarea value="test value"></textarea>
```

但是在 Vue.js 中， 以下代码能成功绑定到 value property 并显示在多行文本框中：

```html
<textarea :value="'test value'"></textarea>
```

**特殊情况使用 `:value.prop`**
以上 Vue.js 源码需要注意的还有，强制作为 property， 还要满足 `!el.component`，即不为动态组件，因为动态组件的 el.component 的值为其 `is attribute` 的值

即动态组件的的 `v-bind` 默认都是作为 attribute 的，如果要作为 property，就要使用 `.prop`，例如：

```html
<div id="app">
  <component :is="element" :value.prop="'test value'"></component>
  <button @click="change">Change</button>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
let app = new Vue({
  el: '#app',
  data: {
    element: 'input'
  },
  methods: {
    change () {
      this.element = 'input' === this.element ? 'textarea' : 'input';
    }
  }
});
</script>
```

如果以上 component 中，删除 `:value.prop` 的 `.prop`，切换到 textarea 时，其值就不会显示在多行文本框中，可以在此页面点击切换标签查看。

##### 总结
- 作为 attribute 和 property 的 `value` 的绑定关系会在用户交互更新值后失效；
- Vue.js 一般使用 `:value` 即可让 `value` 作为 property；
- Vue.js 动态模版需要使用 `:value.prop` 才可让 `value` 作为 property；

#### 使用 Javascript 表达式
迄今为止，在我们的模板中，我们一直都只绑定简单的 property 键值。但实际上，对于所有的数据绑定，Vue.js 都提供了完全的 JavaScript 表达式支持。

```html
<template>
  {{number / 10}}
  {{isOK ? '确定' : '取消'}}
  {{text.split(',').reverse().join(',')}}
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
        number: 100,
        isOK: false,
        text: '123,456'
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

### 指令
指令 (Directives) 是带有 `v-` 前缀的特殊 attribute。指令 attribute 的值预期是单个 JavaScript 表达式 (`v-for` 和 `v-on` 是例外情况，稍后我们再讨论)。指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM。

举个例子：

```html
<p v-if="seen">现在你看到我了</p>
```
这里，`v-if` 指令将根据表达式 `seen` 的值的真假来插入/移除 `<p>` 元素。

#### 参数
`v-bind` 指令可以用于响应式地更新 HTML attribute：

```html
<a v-bind:href="url"> ... </a>
```
在这里 `href` 是参数，告知 `v-bind` 指令将该元素的 `href` attribute 与表达式 `url` 的值绑定。

`v-on` 指令用于监听 DOM 事件：

```html
<a v-on:click="doSomething"> ... </a>
```
在这里参数是监听的事件名。

#### 动态参数
动态参数就是在指令参数中使用 JavaScript 表达式，方法是用方括号括起来：

```html
<a v-bind:[attributeName]="url"> ... </a>
```
这里的 `attributeName` 会被作为一个 JavaScript 表达式进行动态求值，求得的值将会作为最终的参数来使用。例如，如果你的组件实例有一个 data property `attributeName`，其值为 `"href"`，那么这个绑定将等价于 `v-bind:href`。

同样地，你可以使用动态参数为一个动态的事件名绑定处理函数：

```html
<a v-on:[eventName]="doSomething"> ... </a>
```

在这个示例中，当 `eventName` 的值为 `"focus"` 时，`v-on:[eventName]` 将等价于 `v-on:focus`；

#### 修饰符
修饰符 (modifier) 是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。

指令原本就是很方便的东西，而指令修饰符会让指令变得更加方便。

语法：`指令名称:参数.修饰符 = 值`；

例：`v-bind:value.number = "msg"`

**注意：**
- 不同的指令有不同的参数，也有不同的修饰符；
- 有些指令是没有修饰符的；
- 某些指令直接的修饰符会重复，但是使用时需要去查看对应的指令的 api；

**示例：**

实现修改 input 框里边的值后会在页面加载显示的功能：
```html
<body>
    <div id="app">
        <input type="text" v-model="val">
		<span> {{val}} </span>
    </div>
    <script>
        let app = new Vue({
            el:"#app",
            data:{
                val:1
            }
        })
    </script>
</body>
```

但是我们如果想要输入完且失去焦点后才加在到页面的话，我们就需要用到指令修饰符了：

```html
<input type="text" v-model.lazy="val">
```

这时就可以完成上述需求。

再看一种场景：

```html
<body>
    <div id="app">
        <input type="text" v-model = "v1">
        +
        <input type="text" v-model = "v2">
        =
        {{v1+v2}}
    </div>
    <script>
        let app = new Vue({
            el:"#app",
            data:{
                val:1,
                v1:1,
                v2:1
            }
        })
    </script>
</body>
```
浏览器反馈：
![](https://img-blog.csdnimg.cn/b8485ae83102473887e659996860dde9.png)
我们这时如果在 input 框里修改 value 值后，等号后边会自动变为字符串拼接：
![](https://img-blog.csdnimg.cn/d429c38bb8ec41e7b26f02c4c01913ed.png)
这时，我们只需要给 `v-model` 添加一个修饰符 `number` 就可以了：

```html
<input type="text" v-model.number = "v1"> 
+ 
<input type="text" v-model.number = "v2"> 
= 
{{v1+v2}}
```
![](https://img-blog.csdnimg.cn/d724b9b848ce4968ade9c53727c905ef.png)
**补充**

修饰符是可以连用的！

例如：

```html
<input type="text" v-model.number.lazy = "v1"> 
+ 
<input type="text" v-model.number.lazy = "v2"> 
= 
{{v1+v2}}
```

#### 自定义指令
在面对我们想要用到指令去完成一些需求且内置指令处理不了的时候，我们可以制定一个自定义指令，根据我们的开发需求和开放场景来封装一个：

自定义指令分为全局指令与局部指令，区别仅在于有效范围：
- 全局指令的有效范围：在整个 script 标签内可以通用
- 局部指令的有效范围：仅在于 vue 的实例化对象里边

我们可以通过 input 框自动获取焦点这个案例来了解一下自定义指令：

**代码示例：**

```html
let app = new Vue({
	el: "#app",
	directives: {
		focus: {
			// 指令的定义
			inserted: function (el) {
				el.focus()
			}
		}
	}
});
```

```html
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
	// 当被绑定的元素插入到 DOM 中时……
	inserted: function (el) {
    	// 聚焦元素
    	el.focus()
	}
})
```
现在我们已经注册了一个全局的自定义指令，我们只需要在需要使用的元素里加上 `v-focus` 即可：

```html
<input type="text" v-focus> 
```

### 缩写
#### v-bind 缩写

```html
<!-- 完整语法 -->
<a v-bind:href="url"> ... </a>

<!-- 缩写 -->
<a :href="url"> ... </a>

<!-- 动态参数的缩写 -->
<a :[key]="url"> ... </a>
```

#### v-on 缩写

```html
<!-- 完整语法 -->
<a v-on:click="doSomething"> ... </a>

<!-- 缩写 -->
<a @click="doSomething"> ... </a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
```

它们看起来可能与普通的 HTML 略有不同，但 `:` 与 `@` 对于 attribute 名来说都是合法字符，在所有支持 Vue 的浏览器都能被正确地解析。而且，它们不会出现在最终渲染的标记中。

### Data Property 和方法
#### Data Property
组件的 `data` 选项是一个函数。Vue 在创建新组件实例的过程中调用此函数。它应该返回一个对象，然后 Vue 会通过响应性系统将其包裹起来，并以 `$data` 的形式存储在组件实例中。为方便起见，该对象的任何顶级 property 也直接通过组件实例暴露出来：

```html
const app = Vue.createApp({
  data() {
    return { count: 4 }
  }
})

const vm = app.mount('#app')

console.log(vm.$data.count) // => 4
console.log(vm.count)       // => 4

// 修改 vm.count 的值也会更新 $data.count
vm.count = 5
console.log(vm.$data.count) // => 5

// 反之亦然
vm.$data.count = 6
console.log(vm.count) // => 6
```

这些实例 property 仅在实例首次创建时被添加，所以你需要确保它们都在 `data` 函数返回的对象中。必要时，要对尚未提供所需值的 property 使用 `null`、`undefined` 或其他占位的值。

直接将不包含在 `data` 中的新 property 添加到组件实例是可行的。但由于该 property 不在背后的响应式 `$data` 对象内，所以 Vue 的响应性系统不会自动跟踪它。

Vue 使用 `$` 前缀通过组件实例暴露自己的内置 API。它还为内部 property 保留 `_` 前缀。你应该避免使用这两个字符开头的的顶级 `data` property 名称。

#### 方法
我们用 `methods` 选项向组件实例添加方法，它应该是一个包含所需方法的对象：

```html
const app = Vue.createApp({
  data() {
    return { count: 4 }
  },
  methods: {
    increment() {
      // `this` 指向该组件实例
      this.count++
    }
  }
})

const vm = app.mount('#app')

console.log(vm.count) // => 4

vm.increment()

console.log(vm.count) // => 5
```

Vue 自动为 `methods` 绑定 `this`，以便于它始终指向组件实例。这将确保方法在用作事件监听或回调时保持正确的 `this` 指向。在定义 `methods` 时应避免使用箭头函数，因为这会阻止 Vue 绑定恰当的 `this` 指向。

这些 `methods` 和组件实例的其它所有 property 一样可以在组件的模板中被访问。在模板中，它们通常被当做事件监听使用：

```html
<button @click="increment">Up vote</button>
```
在上面的例子中，点击 `<button>` 时，会调用 `increment` 方法。

也可以直接从模板中调用方法。

##### 防抖和节流
Vue 没有内置支持防抖和节流，但可以使用 Lodash 等库来实现。

如果某个组件仅使用一次，可以在 `methods` 中直接应用防抖：

```html
<script src="https://unpkg.com/lodash@4.17.20/lodash.min.js"></script>
<script>
  Vue.createApp({
    methods: {
      // 用 Lodash 的防抖函数
      click: _.debounce(function() {
        // ... 响应点击 ...
      }, 500)
    }
  }).mount('#app')
</script>
```
但是，这种方法对于可复用组件有潜在的问题，因为它们都共享相同的防抖函数。为了使组件实例彼此独立，可以在生命周期钩子的 `created` 里添加该防抖函数：

```html
app.component('save-button', {
  created() {
    // 用 Lodash 的防抖函数
    this.debouncedClick = _.debounce(this.click, 500)
  },
  unmounted() {
    // 移除组件时，取消定时器
    this.debouncedClick.cancel()
  },
  methods: {
    click() {
      // ... 响应点击 ...
    }
  },
  template: `
    <button @click="debouncedClick">
      Save
    </button>
  `
})
```

### 计算属性和侦听器
#### 计算属性
模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。

例如，有一个嵌套数组对象：

```html
Vue.createApp({
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  }
})
```
我们想根据 `author` 是否已经有一些书来显示不同的消息

```html
<div id="computed-basics">
  <p>Has published books:</p>
  <span>{{ author.books.length > 0 ? 'Yes' : 'No' }}</span>
</div>
```
此时，模板不再是简单的和声明性的。你必须先看一下它，然后才能意识到它执行的计算取决于 `author.books`。如果要在模板中多次包含此计算，则问题会变得更糟。

所以，对于任何包含响应式数据的复杂逻辑，你都应该使用**计算属性**。

##### 基本例子

```html
<div id="computed-basics">
  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>
</div>
```

```html
Vue.createApp({
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  },
  computed: {
    // 计算属性的 getter
    publishedBooksMessage() {
      // `this` points to the vm instance
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  }
}).mount('#computed-basics')
```
运行结果如下：
![](https://img-blog.csdnimg.cn/660dbe696deb467c8d85a421b5368639.png)
这里声明了一个计算属性 `publishedBooksMessage`。

尝试更改应用程序 `data` 中 `books` 数组的值，你将看到 `publishedBooksMessage` 如何相应地更改。

你可以像普通属性一样将数据绑定到模板中的计算属性。Vue 知道`vm.publishedBookMessage` 依赖于 `vm.author.books`，因此当 `vm.author.books` 发生改变时，所有依赖 `vm.publishedBookMessage` 绑定也会更新。而且最妙的是我们已经声明的方式创建了这个依赖关系：计算属性的 getter 函数没有副作用，这使得更易于测试和理解。

##### 计算属性缓存 vs 方法
我们可以通过在表达式中调用方法来达到同样的效果：

```html
<p>{{ calculateBooksMessage() }}</p>
```

```html
// 在组件中
methods: {
  calculateBooksMessage() {
    return this.author.books.length > 0 ? 'Yes' : 'No'
  }
}
```
我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。然而，不同的是**计算属性是基于它们的反应依赖关系缓存的**。计算属性只在相关响应式依赖发生改变时它们才会重新求值。这就意味着只要 `author.books` 还没有发生改变，多次访问 `publishedBookMessage` 计算属性会立即返回之前的计算结果，而不必再次执行函数。

这也同样意味着下面的计算属性将不再更新，因为 Date.now () 不是响应式依赖：

```html
computed: {
  now() {
    return Date.now()
  }
}
```
相比之下，每当触发重新渲染时，调用方法将总会再次执行函数。

我们为什么需要缓存？假设我们有一个性能开销比较大的计算属性 `list`，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算属性依赖于 `list`。如果没有缓存，我们将不可避免的多次执行 `list` 的 getter！如果你不希望有缓存，请用 `method` 来替代。

##### 计算属性的 Setter
计算属性默认只有 getter，不过在需要时你也可以提供一个 setter：

```html
// ...
computed: {
  fullName: {
    // getter
    get() {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set(newValue) {
      const names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
// ...
```
现在再运行 `vm.fullName = 'John Doe'` 时，setter 会被调用，`vm.firstName` 和 `vm.lastName` 也会相应地被更新。

#### 侦听器
虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器。这就是为什么 Vue 通过 `watch` 选项提供了一个更通用的方法，来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

例如：

```html
<div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
</div>
```

```html
<!-- 因为 AJAX 库和通用工具的生态已经相当丰富，Vue 核心代码没有重复 -->
<!-- 提供这些功能以保持精简。这也可以让你自由选择自己更熟悉的工具。 -->
<script src="https://cdn.jsdelivr.net/npm/axios@0.12.0/dist/axios.min.js"></script>
<script>
  const watchExampleVM = Vue.createApp({
    data() {
      return {
        question: '',
        answer: 'Questions usually contain a question mark. ;-)'
      }
    },
    watch: {
      // whenever question changes, this function will run
      question(newQuestion, oldQuestion) {
        if (newQuestion.indexOf('?') > -1) {
          this.getAnswer()
        }
      }
    },
    methods: {
      getAnswer() {
        this.answer = 'Thinking...'
        axios
          .get('https://yesno.wtf/api')
          .then(response => {
            this.answer = response.data.answer
          })
          .catch(error => {
            this.answer = 'Error! Could not reach the API. ' + error
          })
      }
    }
  }).mount('#watch-example')
</script>
```
![](https://img-blog.csdnimg.cn/883ef6fe368f46f88d0b208d7c2453e8.png)
在这个示例中，使用 `watch` 选项允许我们执行异步操作 (访问一个 API)，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。

##### 计算属性 vs 侦听器
Vue 提供了一种更通用的方式来观察和响应当前活动的实例上的数据变动：**侦听属性**。当你有一些数据需要随着其它数据变动而变动时，你很容易滥用 `watch`——特别是如果你之前使用过 AngularJS。然而，通常更好的做法是使用计算属性而不是命令式的 `watch` 回调。细想一下这个例子：

```html
<div id="demo">{{ fullName }}</div>
```

```html
const vm = Vue.createApp({
  data() {
    return {
      firstName: 'Foo',
      lastName: 'Bar',
      fullName: 'Foo Bar'
    }
  },
  watch: {
    firstName(val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName(val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
}).mount('#demo')
```
上面代码是命令式且重复的。将它与计算属性的版本进行比较：

```html
const vm = Vue.createApp({
  data() {
    return {
      firstName: 'Foo',
      lastName: 'Bar'
    }
  },
  computed: {
    fullName() {
      return this.firstName + ' ' + this.lastName
    }
  }
}).mount('#demo')
```
代码就简化很多；