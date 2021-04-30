# 第六讲 表单相关控件

## v-model指令

实现双向的绑定

你可以用 `v-model` 指令在表单 `<input>`、`<textarea>` 及 `<select>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但 `v-model` 本质上不过是语法糖。**它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理**。

`v-model` 会忽略所有表单元素的 `value`、`checked`、`selected` attribute 的初始值而总是将 Vue 实例的数据作为数据来源。你应该通过 JavaScript 在组件的 `data` 选项中声明初始值。

`v-model` 在内部为不同的输入元素使用不同的 property 并抛出不同的事件：

- text 和 textarea 元素使用 `value` property 和 `input` 事件；
- checkbox 和 radio 使用 `checked` property 和 `change` 事件；
- select 字段将 `value` 作为 prop 并将 `change` 作为事件。

对于需要使用[输入法](https://zh.wikipedia.org/wiki/输入法) (如中文、日文、韩文等) 的语言，你会发现 `v-model` 不会在输入法组合文字过程中得到更新。如果你也想处理这个过程，请使用 `input` 事件。

### 复选框

这里需要注意的是，多个复选框会得到一个数组的集合

````vue
    <p><input type="checkbox" v-model="p" value='one'>任务1</p>
    <p><input type="checkbox" v-model="p" value='two'>任务1</p>
    <p><input type="checkbox" v-model="p" value='three'>任务1</p>
````

````jsx
data:fucntion(){
   return {
       p:['two'],
    }
}
````

这里的数组，表示第二个被默认选中。

![mark](http://qiniu.cloud-zhi.com/blog/210422/FjiK6ea3mF.png?imageslim)

### 修饰符

####  .lazy

在默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步 (除了[上述](https://cn.vuejs.org/v2/guide/forms.html#vmodel-ime-tip)输入法组合文字时)。你可以添加 `lazy` 修饰符，从而转为在 `change` 事件_之后_进行同步：

```vue
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg">
```

#### .number

如果想自动将用户的输入值转为数值类型，可以给 `v-model` 添加 `number` 修饰符：

```
<input v-model.number="age" type="number">
```

这通常很有用，因为即使在 `type="number"` 时，HTML 输入元素的值也总会返回字符串。如果这个值无法被 `parseFloat()` 解析，则会返回原始的值。

#### .trim

如果要自动过滤用户输入的首尾空白字符，可以给 `v-model` 添加 `trim` 修饰符：

```
<input v-model.trim="msg">
```