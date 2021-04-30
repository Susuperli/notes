# 第十讲 高阶组件

高阶组件就是一个没有副作用的**纯函数**

react中副作用操作

- 发送ajax请求数据
- 设置订阅/启动定时器
- 手动更改真实DOM

## 我可以使用高阶组件做什么呢？

概括的讲，高阶组件允许你做：

- 代码复用，逻辑抽象，抽离底层准备（bootstrap）代码
- 渲染劫持
- State 抽象和更改
- Props 更改

属性代理的实现方法如下：

```jsx
function ppHOC(WrappedComponent) {
  return class PP extends React.Component {
    render() {
      return <WrappedComponent {...this.props}/>
    }
  }
}
```

可以看到，这里高阶组件的 render 方法**返回**了一个 type 为 WrappedComponent 的 React Element（也就是被包装的那个组件），我们把高阶组件收到的 props 传递给它，因此得名 **Props Proxy**。

注意：

```kotlin
<WrappedComponent {...this.props}/>
// is equivalent to
React.createElement(WrappedComponent, this.props, null)
```

它们都创建了一个 React Element，描述了 React 在『reconciliation』（可以理解为解析）阶段的渲染内容，如果你想了解更多关于 React Element 的内容，请看 [Dan Abramov 的这篇博客](https://link.jianshu.com?t=https://facebook.github.io/react/blog/2015/12/18/react-components-elements-and-instances.html) 和官方文档上关于 [reconciliation process](https://link.jianshu.com?t=https://facebook.github.io/react/docs/reconciliation.html) 的部分