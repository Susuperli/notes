# 第四讲 计算和监听属性以及事件修饰符

## 侦听属性Watch

模板内的表达式非常便利，设计它们的初衷就是用于简单运算的，放入太多逻辑会让模板难以维护。**Vue提供了一种更通用的方法来观察响应实例上的数据变动**：侦听属性。当你有一些数据要随着其他数据变换而变化时。**一个watch函数只能侦听一个值的变化。**

````jsx
  watch:{
    dog:function(value){
      this.dog=value.toUpperCase()
    }
  }
````

## 计算属性

使用侦听属性，只能针对指定的数据，无法重用，对于复杂逻辑可以使用计算属性。

计算属性是用来声明式的描述一个值依赖了其他值。当你在模板里面把数据绑定发哦一个计算属性上面，vue会其依赖的任何值导致该计算属性改变时更新DOM。这个功能非常强大，他可以让你的代码更加声名式、数据驱动并且容易维护

````jsx
  computed:{
    sum:function(){
      let s=this.dog+this.cat;
      return s;
    }
  },
````

### methods和computed区别

我们可以使用methods来代替computed，效果上两个都是一样的，但是computed是基于它的**依赖缓存**，只有相关依赖发生改变时才会重新取值。而使用methods，再重新渲染的时候，函数总会重新调用执行。可以说使用computed性能会更好，但是如果你不希望缓存，你可以使用methods属性。

使用methods，在调用时要写方法的调用方式，方法名()。

## 事件修饰符

在事件处理程序中调用 `event.preventDefault()` 或 `event.stopPropagation()` 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。

为了解决这个问题，Vue.js 为 `v-on` 提供了**事件修饰符**。之前提过，修饰符是由点开头的指令后缀来表示的。

- `.stop`
- `.prevent`
- `.capture`
- `.self`
- `.once`
- `.passive`

```vue
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 `v-on:click.prevent.self` 会阻止**所有的点击**，而 `v-on:click.self.prevent` 只会阻止对元素自身的点击。

> 2.1.4 新增

```vue
<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>
```

不像其它只能对原生的 DOM 事件起作用的修饰符，`.once` 修饰符还能被用到自定义的[组件事件](https://cn.vuejs.org/v2/guide/components-custom-events.html)上。如果你还没有阅读关于组件的文档，现在大可不必担心。

> 2.3.0 新增

Vue 还对应 [`addEventListener` 中的 `passive` 选项](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#Parameters)提供了 `.passive` 修饰符。

```vue
<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
```

这个 `.passive` 修饰符尤其能够提升移动端的性能。

不要把 `.passive` 和 `.prevent` 一起使用，因为 `.prevent` 将会被忽略，同时浏览器可能会向你展示一个警告。请记住，`.passive` 会告诉浏览器你*不*想阻止事件的默认行为。