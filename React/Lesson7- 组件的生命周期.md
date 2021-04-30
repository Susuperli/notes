# 第七讲 组件的生命周期

## 简介

在组件的整个生命周期中，随着该组件的props或者state发生改变，它的DOM表现也将有相应的改变，一个组件就是一个状态机，罪域待定的输入，他总会返回一个的输出。

React为每个组件提供生命周期钩子函数去响应不同时刻——实例化期、存在期及销毁时。

**钩子函数：**钩子函数是在一个事件触发的时候，在系统级捕获到了他，然后做一些操作。一段用以处理系统消息的程序。“钩子”就是在某个阶段给你一个做某些处理的机会

## 组件的生命周期（旧）

- 生命周期的方法
- 实例化期 存在期 销毁期
- 组件被实例化的时候
- 组件状态被改变的时候
- 组件被销毁的时候

![mark](http://qiniu.cloud-zhi.com/blog/210421/1I7G7kk14C.png?imageslim)

### 实例化期

首次调用组件时，有以下方法会被调用（注意顺序，从上到下先执行）

- getDefaultProps

  这个方法使用来设置组件磨人的props，组件生命周期只会调用一次。但是只适合React.createClass直接创建的组件，使用ES6/ES7创建的这个方式不可使用

  ````React
  //es7
  class Component{
      static defaultProps={}
  }
  
  //或者也可以在外面
  //Compenent.defaultProps
  ````

- componentWillMount

  第一次渲染阶段在调用render方法前被调用

  作用：该方法在整个组件声明周期只会被调用一次，所以可以利用该方法做一些组件内部的初始化工作，这个是在render方法调用前可以修改state的最后一次机会。（不会导致组件重新渲染）

- render

  jsx通过这里，解析成对应的虚拟DOM，渲染成最终效果。

- **componentDidMount**

  第一次渲染成功后，组件对应的dom已经添加到页面后调用

  作用：这个阶段表示组件对应的DOM已经存在，我们可以在这个时候做一些依赖DOM的操作或者其他的一些如请求数据和第三方库整合的操作。如果嵌套了子组件，子组件会比父组件优先渲染，所以这个时候可以获取子组件对应的DOM。

#### 关于React中获取为什么一定要在componentDidMount

- constructor()中获取数据的话，如果时间太长，或者出错，组件就会渲染不出来，整个页面都没法渲染。constructor是组件state来初始化工作，并不是设计来加载数据的。
- 如果使用SSR(服务端渲染)，componentWillMount会执行2次，一次在服务端，一次在客户端。而componentDidMount不会。
- React16之后采用了Fiber架构，只有componentDidMount生命周期函数是确定被执行一次的,类似ComponentWillMount的生命周期钩子都有可能执行多次，所以不加以在这些生命周期中做有副作用的操作,比如请求数据之类。
- componentDidMount万法中的代码，是在组件已经完全挂载到网页上才会调用被执行，所以可以保证数据的加载。此外，在这方法中调用setState方法，会触发重渲染。所以，官方设计这个方法就是用来加载外部数据用的,或处理其他的副作用代码。

### 更新期

#### componentWillReceiveProps

componentWillReceiveProps(newProps)

条件：当组件或得新属性的时候，第一次渲染不会触发

用处：可以用来根据新的属性来修改组件状态

#### shouldComponentUpData

shouldComponentUpData(newProps,newState)

条件：接收到新属性或者新状态时会触发，除了forceUpdata和初始化渲染。

用处：该方法让我们有机会决定是否重新渲染组件，如果返回false，那么不会重新渲染组件，是react性能优化非常重要的一环，组件接收新的state或者props时调用，我们可以设置在此对前后两个props和state是否相同，如果相同则返回false组织更新，因为相同的属性状态一定会生成相同的dom树，这样就不需要创造新的dom树和旧的dom树进行diff算法对比，节省大量性能，尤其是在都没结构恢复的时候

#### componentWillUpData

条件：当组件确定要更新的时候，在render之前调用。

用处：这个方法可以确定一定会更新组件，可以执行更新前的操作。

注意：方法中不能使用setState，setState的操作应该在componentWillReceiveProps方法中调用

#### render

渲染

#### componentDidUpData

条件：更新到应用到DOM之后。

用处：这个方法更新真实的DOM成功之后调用，当我们需要访问真实的DOM时，这个方法也就经常能用到

### 挂载期

#### componentWillUnmount

每当组件完成，这个组件就必须从DOM中销毁，此时该方法就会被调用。当我们在组件中使用了setInterval，那我们就需要在这个方法中调用clearInterval。

![mark](http://qiniu.cloud-zhi.com/blog/210421/HjAdhC3dC0.png?imageslim)

![mark](http://qiniu.cloud-zhi.com/blog/210421/8Cj0aAkJDg.png?imageslim)

## 组件的生命周期（新）

### 实例化期

#### getDerivedStateFromProps

getDerivedStateFromProps(pros,state)

组件每次被render的时候，包括在组件构建之后（虚拟dom之后，实际dom挂载之前），每次获取新的props或者state之后，每次接收新的props之后都会返回一个新的对象作为新的state，返回null则说明不需要更新state；配合componentDidUpdata，可以覆盖componentWillRecaiveProps的所有用法。

**需要static定义。**

#### render

#### shouldComponentUpdata(props,state)

#### render

#### getSnapshotBeforeUpdata(prevProps,prevState)

触犯时间：updata发生的时候，在render之后，在组件dom渲染之前；返回一个值，作为componentDidUpdata的带三个参数；配合componentDidUpdata，可以覆盖componentWillUpdata所有用法。

#### componentDidMount()

### 更新期

#### getDerivedStateFromProps

#### shouldComponentUpdata

#### render

#### getSnapBeforeUpdata(prevProps,prevState)

#### componentDidUpdata()

### 卸载期

#### componentWillUnmount

![mark](http://qiniu.cloud-zhi.com/blog/210421/H3jH4Jk13J.png?imageslim)

## 变更原因

- 原来的生命周期的生命周期在React v16提出的Fiber之后就不合适了，因为如果要开启async rendering，在render函数之前的所有函数，都有可能被渲染多次。
- 如果开发者开了async rendering，而且有在以上这些render前执行的生命周期方法做AJAx请求的话，那ajax将被调用多次，而且在componentWillMount里发起ajax，不管多快得到结果也赶不上首次render，而且componentWillMount在服务器端渲染也会被调用到，所了除了shouldComponentUpdata，其他在render函数之前的所有函数（componentWillMount，componentWillReceiveProps，componentWillUpdata）都被getDerivedStataFromProps代替，也就是用一个静态函数getDerivedStateFromProps来代替被取代的几个生命周期函数，就是强制开发者在render之前只做无副作用的操作，而且能做的操作局限根据props和state决定新的state。

## 新旧周期的比较

![mark](http://qiniu.cloud-zhi.com/blog/210421/7IKHIaGF1d.png?imageslim)





