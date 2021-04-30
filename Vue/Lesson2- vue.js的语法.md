# 第二讲 vue.js的语法

## vue.js的模板语法

- 使用了基于html的模板语法，允许开发者声明式将DOM绑定在底层vue实例的数据。
- 核心是一个允许你采用简洁的模板来声明式的将数据渲染仅dom的系统
- 结合相应系统，在应用状态改变时，vue能够只智能地计算出重新渲染组件的最小代价应用DOM操作上。

### data中为什么要用函数

反复调用时作用域的问题。

### 主要内容

#### 插值

- 文本

  数据绑定最常见的形式就是使用{{}}（双大括号）

  `````jsx
  <div>
    <p>{{message}}</p>
</div>
  `````

- 纯html

  使用v-html指令输出html代码（浏览器会自动解析成HTML标记）

  ````jsx
  <div v-html='message'></div>
  ````

- 属性

  HTML属性中的值使用v-bind指令进行绑定

  v-bind:属性名="{'属性名':布尔值}"，当布尔值为true时应用该属性值，否者不用该值

  ````jsx
  <p v-bind:class="{bg:isA}">这是一个标题</p>
  
   <p v-bind:class={bg:show}>我叫吕泽准</p>
  ````

- 使用js表达式

  在我们的模板中，我们一直都在只绑定简单的属性键值。但实际上，对于所欲的数据绑定，vue.js都提供了完全的js表达式
  
  ````jsx
  <div id='app'>
      {{5+5}}<br/>
      {{ok?'yes':'no'}}
      {{message.split('')}}
      <div v-bind:id='"list"+id'></div>
  </div>
  ````
  
  表达式是由运算符构成，并运算产生结果的语法结构，循环语句和if语句是典型的语法结构。

#### 指令

是指带有v-前缀的特殊属性。指令属性的值预期是单一js表达式（除了v-for，之后再讨论）。指令的职责就是当其表达式的值改变时相应的将某些行为应用到dom上。

````jsx
<p v-if=seen>加入我叫吕泽准</p>  //当seen的值为true时插入该标记，否则不插入
````

##### 参数

一些指令能接受一个参数，在指令名称之后以冒号表示。例如，v-bind指令可以用于响应式的更新HTML特征：

````jsx
<a v-bind:href='url'></a>
````

在这里href是参数，告知v-bind指令将该元素的href特性与表达式url的值绑定。

另一个例子是v-on指令，它用于绑定事件，监听DOM事件

```jsx
<a v-on:click="doSomething"></a>
```

在这里参数是监听的事件名。

##### 缩写

vue.js为这两个最常用的指令提供特别的缩写

````jsx
<!-- 完整语法 -->
<a v-bind:href="url">...</a>

<!-- 缩写 -->
<a :href="url">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a :[key]="url"> ... </a>
````

````jsx
<!-- 完整语法 -->
<a v-on:click="doSomething">...</a>

<!-- 缩写 -->
<a @click="doSomething">...</a>

<!-- 动态参数的缩写 (2.6.0+) -->
<a @[event]="doSomething"> ... </a>
````

##### 修饰符

修饰符 (modifier) 是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，`.prevent` 修饰符告诉 `v-on` 指令对于触发的事件调用 `event.preventDefault()`：

```jsx
<form v-on:submit.prevent="onSubmit">...</form>
```

1.事件修饰符
1）.stop
作用：调用event.stop，阻止事件冒泡

<div id="app">
    <div @click="fatherClick">
        <button @click.stop="childClick">click</button>
    </div>
</div>
``````jsx
const vm = new Vue({
    el: '#app',
    methods: {
        fatherClick() {
            console.log('father');
        },
        childClick() {
            console.log('child');
        }
    }
})
``````

【结果】若没有阻止冒泡则打印child，father，组织后只打印child 

2）.prevent
作用：调用event.preventDefault()，阻止默认事件，举个栗子，form表单在提交时，会自动刷新页面，如图1

图1 未阻止默认事件
此时需要阻止默认事件，如下

<div id="app">
    <!-- 方法1 -->
    <form @submit.prevent="onSubmit">
        <input type="submit" value="submit">
    </form>
    <!-- 方法2：只写修饰符 -->
    <form v-on:submit.prevent>
        <input type="submit">
    </form>
</div>
````````jsx
const vm = new Vue({
    el: '#app',
    methods: {
        onSubmit() {
            console.log('submit')
        }
    }
})
````````


图2 方法1结果
3）.capture
作用：事件捕获模式

<div id="app">
    <div @click.capture="fatherClick">
        <button @click="childClick">click</button>
    </div>
</div>
【结果】点击click，打印结果如下

```````jsx
const vm = new Vue({
    el: '#app',
    methods: {
        fatherClick() {
            console.log('father');
        },
        childClick() {
            console.log('child');
        }
    }
})
```````

4）.self
作用：只当事件是从侦听器绑定的元素本身触发时才触发回调

<div id="app">
    <div :style="{ backgroundColor: '#f88', width:'100px',height:'100px'}" @click.self='fatherClick'>
        <button  @click='childClick'>click</button>
    </div>
</div>
``````jsx
const vm = new Vue({
    el: '#app',
    methods: {
        fatherClick() {
            console.log('father');
        },
        childClick() {
            console.log('child');
        }
    }
})
``````

5）.once
作用：只触发一次回调，2.1.4新增

<div id="app">
    <button @click.once="print">click</button>
</div>
`````jsx
const vm = new Vue({
    el: '#app',
    methods: {
        print() {
            console.log('button')
        }
    }
})
`````

6）.passive
作用：设置addEventListener中的passive选项，2.3.0版本中新增的，能够提升移动端的性能。在触发触摸事件时，即使执行了一个空的函数，也会让页面卡顿。因为浏览器不知道监听器到底会不会阻止默认事件，所以浏览器要等到执行完整个函数后，才能决定是否要滚动页面。passive事件监听器，允许开发者告诉浏览器，监听器不会阻止默认行为，从而浏览器可以放心大胆的滚动页面，这样可以大幅度提升移动端页面的性能，因为据统计只有20%的触摸事件会阻止默认事件。passive会告诉浏览器你不想阻止默认事件的默认行为

【注意】

① 使用修饰符时，顺序很重要。相应的代码会以同样的顺序产生。因此，

v-on:click.prevent.self //会阻止所有的点击的默认事件
v-on:click.self.prevent //只会阻止元素自身点击的默认事件
② 不要把.passive 和.prevent 一起使用，因为.prevent将会被忽略，同时浏览器可能会向你展示一个警告

#### Filters过滤器

该功能在vue3.0中已经被废弃
