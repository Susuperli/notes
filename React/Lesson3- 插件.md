# 第三讲 插件

## JSX语法介绍

- React的核心机制之一就是可以在内存中创建虚拟的DOM元素。React利用虚拟DOM来减少对实际DOM的操作从来提升性能。

### JSX本质

创建jsx语法的本质目的是为了使用基于cml的方式表达组件的嵌套，保持和HTML一致的结构，语法除了在描述组件上比较特别以外，其他和普通的JavaScript没有区别。并最终所有的jsx都会编译成原生的JavaScript。

### 创建虚拟dom的两种方式

#### jsx方式

`````react
const Vdom=<h1 id="test">hello</h1> //使用小括号作为整体可以换行书写
  ReactDOM.render(Vdom,document.getElementById("root"))
`````

#### react原生方式

### JSX语法

- 全称：JavaScript XML
- React定义的一种类似与XML的扩展语法js+xml
- 本质是React.creatElement(component,props,...)
- 作用：用来简化创建虚拟dom
  - 写法：var ele=\<h1>hello\</h1>
  - 注意：他不是字符串，也不是html/xml标签
  - 他最终产生的就是一个js对象
- 定义虚拟dom，不要写引号。
- 标签中混入js时要用{}
- 样式的类型指定不要用class，要用className
- 虚拟dom必须只能有一个根标签
- 标签必须闭合
- 标签首字母
  - 若小写字母开头，则将会把标签转换为html同名标签，若无标签对应的元素，则报错。
  - 若大写开头，react将其识别为组件，就去渲染组件，若没有该组件，则报错。
- jsx允许在模板中插入数组，数组会自动展开所有成员。

