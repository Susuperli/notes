# 第九讲 边界处理情况

## 访问父级组件实例

和 `$root` 类似，`$parent` property 可以用来从一个子组件访问父组件的实例。它提供了一种机会，可以在后期随时触达父级组件，以替代将数据以 prop 的方式传入子组件的方式

其中`$root`会或得根组件的实例，而`$parent`会获得父组件的实例。

## 访问子组件实例或者子元素

尽管存在 prop 和事件，有的时候你仍可能需要在 JavaScript 里直接访问一个子组件。为了达到这个目的，你可以通过 `ref` 这个 attribute 为子组件赋予一个 ID 引用。例如：

````vue
<base-input ref="usernameInput"></base-input>
````

使用如下方法访问，修改

`````jsx
this.$refs.usernameInput
`````

子组件

`````vue
    <Mimi
      :message="message"
      @changeBackground="changebg"
      @getMessage="fromSon"
      ref="mimiyan"
    >
`````

````jsx
    changemimi: function () {
      this.$refs.mimiyan.goodDogs='眯眯眼是傻逼';
    },
````

