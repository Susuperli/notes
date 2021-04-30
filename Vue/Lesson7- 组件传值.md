# 第七讲 组件传值

## 父向子传

主要是通过**props**的方式

## [传递静态或动态 Prop](https://cn.vuejs.org/v2/guide/components-props.html#传递静态或动态-Prop)

像这样，你已经知道了可以像这样给 prop 传入一个静态的值：

```vue
<blog-post title="My journey with Vue"></blog-post>
```

你也知道 prop 可以通过 `v-bind` 动态赋值，例如：

```vue
<!-- 动态赋予一个变量的值 -->
<blog-post v-bind:title="post.title"></blog-post>

<!-- 动态赋予一个复杂表达式的值 -->
<blog-post
  v-bind:title="post.title + ' by ' + post.author.name"
></blog-post>
```

在上述两个示例中，我们传入的值都是字符串类型的，但实际上*任何*类型的值都可以传给一个 prop。

### [传入一个数字](https://cn.vuejs.org/v2/guide/components-props.html#传入一个数字)

```vue
<!-- 即便 `42` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:likes="42"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:likes="post.likes"></blog-post>
```

### [传入一个布尔值](https://cn.vuejs.org/v2/guide/components-props.html#传入一个布尔值)

```vue
<!-- 包含该 prop 没有值的情况在内，都意味着 `true`。-->
<blog-post is-published></blog-post>

<!-- 即便 `false` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:is-published="false"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:is-published="post.isPublished"></blog-post>
```

### [传入一个数组](https://cn.vuejs.org/v2/guide/components-props.html#传入一个数组)

```vue
<!-- 即便数组是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:comment-ids="[234, 266, 273]"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:comment-ids="post.commentIds"></blog-post>
```

### [传入一个对象](https://cn.vuejs.org/v2/guide/components-props.html#传入一个对象)

```vue
<!-- 即便对象是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post
  v-bind:author="{
    name: 'Veronica',
    company: 'Veridian Dynamics'
  }"
></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:author="post.author"></blog-post>
```

### [传入一个对象的所有 property](https://cn.vuejs.org/v2/guide/components-props.html#传入一个对象的所有-property)

如果你想要将一个对象的所有 property 都作为 prop 传入，你可以使用不带参数的 `v-bind` (取代 `v-bind:prop-name`)。例如，对于一个给定的对象 `post`：

```vue
post: {
  id: 1,
  title: 'My Journey with Vue'
}
```

下面的模板：

```vue
<blog-post v-bind="post"></blog-post>
```

等价于：

```vue
<blog-post
  v-bind:id="post.id"
  v-bind:title="post.title"
></blog-post>
```

## [单向数据流](https://cn.vuejs.org/v2/guide/components-props.html#单向数据流)

所有的 prop 都使得其父子 prop 之间形成了一个**单向下行绑定**：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外变更父级组件的状态，从而导致你的应用的数据流向难以理解。

额外的，每次父级组件发生变更时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你**不**应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。

这里有两种常见的试图变更一个 prop 的情形：

1. **这个 prop 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 prop 数据来使用。**在这种情况下，最好定义一个本地的 data property 并将这个 prop 用作其初始值：

   ```jsx
   props: ['initialCounter'],
   data: function () {
     return {
       counter: this.initialCounter
     }
   }
   ```

2. **这个 prop 以一种原始的值传入且需要进行转换。**在这种情况下，最好使用这个 prop 的值来定义一个计算属性：

   ```jsx
   props: ['size'],
   computed: {
     normalizedSize: function () {
       return this.size.trim().toLowerCase()
     }
   }
   ```

注意在 JavaScript 中对象和数组是通过引用传入的，所以对于一个数组或对象类型的 prop 来说，在子组件中改变变更这个对象或数组本身**将会**影响到父组件的状态。

## [Prop 验证](https://cn.vuejs.org/v2/guide/components-props.html#Prop-验证)

我们可以为组件的 prop 指定验证要求，例如你知道的这些类型。如果有一个需求没有被满足，则 Vue 会在浏览器控制台中警告你。这在开发一个会被别人用到的组件时尤其有帮助。

为了定制 prop 的验证方式，你可以为 `props` 中的值提供一个带有验证需求的对象，而不是一个字符串数组。例如：

```jsx
Vue.component('my-component', {
  props: {
    // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
  }
})
```

当 prop 验证失败的时候，(开发环境构建版本的) Vue 将会产生一个控制台的警告。

注意那些 prop 会在一个组件实例创建**之前**进行验证，所以实例的 property (如 `data`、`computed` 等) 在 `default` 或 `validator` 函数中是不可用的。

### [类型检查](https://cn.vuejs.org/v2/guide/components-props.html#类型检查)

`type` 可以是下列原生构造函数中的一个：

- `String`
- `Number`
- `Boolean`
- `Array`
- `Object`
- `Date`
- `Function`
- `Symbol`

额外的，`type` 还可以是一个自定义的构造函数，并且通过 `instanceof` 来进行检查确认。例如，给定下列现成的构造函数：

```jsx
function Person (firstName, lastName) {
  this.firstName = firstName
  this.lastName = lastName
}
```

你可以使用：

```jsx
Vue.component('blog-post', {
  props: {
    author: Person
  }
})
```

来验证 `author` prop 的值是否是通过 `new Person` 创建的。

## 子向父传

父组件：

`````vue
<template>
  <div id="app">
    <div :style="{color:bg}">我是父组件的{{message}}</div>
    <Mimi :message='message' @changeBackground='changebg' ></Mimi>
  </div>
</template>


 methods:{
    changebg:function(data){
      this.bg=data
    }
  },
`````

子组件：

`````vue
<template>
    <div>
        我是子组件的{{message}}
        <button @click='changeBack("red")'>red</button>
        <button @click='changeBack("green")'>green</button>
    </div>
</template>
`````

````jsx
    methods:{
        changeBack:function(c){
            this.$emit('changeBackground',c)
        }
    }
````

## 非父子组件通信

### 中央事件控制总线

单独一个文件new出一个新的vue实例对象

`````jsx
import Vue from 'vue'

export default new Vue();
`````

在两个组件都引入新的实例对象

````jsx
import bus from './../bus.js'
````

通过事件将信息emit出

`````vue
<button @click="transData">点我传值</button>
`````

`````jsx
        transData:function(){
            bus.$emit('changeBus',this.formData)
        }
`````

通过$on方法监听

````jsx
    mounted(){
        bus.$on('changeBus',(value)=>{
            this.getName=value
        })
    }
````

### 插槽

#### 简单使用

父组件

`````vue
    <Mimi :message='message' @changeBackground='changebg' @getMessage='fromSon'>
        <h1>我来自父组件：我是大号的摇摆羊</h1>   //放置要传递的内容
    </Mimi>
`````

子组件

````vue
    <div>
        我是子组件的{{message}}
        <slot />  //放置slot来承接父组件传过来的内容
    </div>
````

#### 编译作用域

**父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。**

#### 后备内容

同上例，作出如下改变

````vue
<slot><h1>我来自子组件：我是默认的眯眯眼</h1></slot>  //设置默认值
````

![mark](http://qiniu.cloud-zhi.com/blog/210423/cgbg2J1f0j.png?imageslim)

照样渲染，默认值不生效

删除父组件内容，默认值才会生效

``````vue
    <Mimi :message='message' @changeBackground='changebg' @getMessage='fromSon'>
    </Mimi>
``````

![mark](http://qiniu.cloud-zhi.com/blog/210423/gH5m4fddJK.png?imageslim)

#### 具名插槽

父组件：使用template作为分隔，使用v-slot:name 来绑定插槽名

````vue
    <Mimi :message='message' @changeBackground='changebg' @getMessage='fromSon'>
        <template v-slot:head>  //使用template作为分隔，使用v-slot:name 来绑定插槽名
          <h1>羊头</h1>
        </template>
        <h1>羊肚子</h1>
        <template v-slot:foot>
           <h1>羊蹄子</h1>
        </template>
    </Mimi>
````

子组件：使用name:name 来接受父组件的传值，默认会传递默认的人。

`````vue
    <div>
        <header>
            <!-- 这里放羊头 -->
            <slot name="head"/> //使用name:name 来接受父组件的传值
        </header>
        <main>
            <!-- 这里放羊肚子，为默认值 -->
            <slot  />
        </main>
        <footer>
            <!-- 这里放羊蹄子 -->
            <slot name="foot"/>
        </footer>
    </div>
`````

![mark](http://qiniu.cloud-zhi.com/blog/210423/5e6dI9LFb6.png?imageslim)

![mark](http://qiniu.cloud-zhi.com/blog/210423/mfFe7d6faA.png?imageslim)

#### 作用域插槽

父组件

`````vue
        <template v-slot:default="slotProps">
           <h1>{{slotProps.user}}</h1>
        </template>
`````

子组件

```vue
            <slot v-bind:user='user'>
            </slot>
```

`````jsx
            user:{
                username:'摇摆羊',
                age:23
            }
`````

![mark](http://qiniu.cloud-zhi.com/blog/210423/Hc1gg9GAdG.png?imageslim)

#### 具名插槽的缩写

参数之前的所有内容 (`v-slot:`) 替换为字符 `#`。例如 `v-slot:header` 可以被重写为 `#header`