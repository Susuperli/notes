# 第九讲 Redux

## 简介

随 JavaScript单页应用开发日趋复杂, JavaScrpt需要管理比任何时候都要多的 state(状态)这些 state可能包括服务器响应、缓存数据本地生成尚未持久化到服务器的数据,也包括U状态,如激活的路由,被选中的标签,是否显示加载动效或者分页器等等
管理不断变化的 state非常困难,尤其是很深层次的组件嵌套,造成 state需要需要互相传递,如果一个 model的变化会引起另一个 model变化,那么当vew变化时,就可能引起对应 model以及另一个 model的变化,依次地,可能会引起另个view的变化,直至你搞不清楚到底发生了什么, state在什么时候,由于什么原因,如何变化已然不受控制,当系统变得错综复杂的时候,想重现问题或者添加新功能就会变得举步维艰。

### redux是什么

- 他是一个专门用于做**状态管理**的js库（不是react的插件库）。
- 他可以在拥有react，angulat，vue等项目中，但基本与react配合使用。
- **作用：集中式管理react应用中多个组件共享状态。**

### 什么时候用

某个组件的状态，需要让其他组件可以随时拿到，需要共享自己的状态（一般在大型的项目中使用）。

一个组件需要改变另外一个组件的状态（通信 ）

能不用就不用，如果数据管理起来比较吃力就考虑使用。

## 三大原则

![mark](http://qiniu.cloud-zhi.com/blog/210421/BA30j1d8jK.png?imageslim)

### 单一数据源

**整个应用的state被存储一颗object tree中，并且这个object tree 只存在唯一一个store中。**

使开发变得非常容易，来自服务端的state可以在无需编写更多的代码情况下被序列化并注入到客户端中，由于是单一的state tree，调试也变得非常容易。在开发中，你可以把应用的state保存到本地，从而加快开发速度。此外，受益于单一的state tree，以前难以实现的如撤销、重做这类功能也变得轻而易举。

### state是只读的

**唯一改变state的方法就是触发action，action是一个用于描述已发生事件的普通对象。**

这样确保了视图和网络请求都不能直接修改state，相反他们只能表达要修改的意图，因为所以的修改都被集中化处理且严格按照一个接一个的顺序执行，因此不用担心race condition的出现。Action就是普通对象而已，因此他们可以被日志打印、序列化、存储、后期调试或测试时放回来。

### 使用纯函数来执行修改

**为了描述action如何改变state tree，你需要编写reducers**

Reducer只是一些纯函数，他接受先前的state和action，并返回新的state，刚开始你可以只有一个reducer，随着应用的变大，你可以把它拆成多个小的reducer，分别独立地操作state tree的不同部分，因为reducer只是函数，你可以控制他们被条用的顺序，传入附加数据，甚至可以编写可复用的reducer来处理一些通用任务，如分页器。

## 函数说明

### action

Action是把数据从应用传到store 的有效载荷。它是store 数据的唯一来源。一般来说会通过store.dispatch()将action传到store。**动作对象。**

- 在Redux中,我们用对象来描述行为
- 行为有很多种，为了以示区别，我们给每个描述行为的对象增加一个type字段， type字段的值就表示当前对象所描述的是哪种具体行为。
- 无论哪一种行为，只要发生了，都会产生几个与该行为相关的最直接最重要的数据。而这些数据也在对象描述行为的范围内，所以添加任务除了type字段外，还需要text字段告诉读者添加了什么任务,也需要id字段方便索引。
- 综上所述，在Redux中，用一种有固定格式的对象来描述行为，这种固定格式体现在:①该对象必须有type字段②该对象的其他字段不做任何限制，但从道理上讲其他字段不会特别多。如果存在,一定都是行为最精华的细节或数据描述
- 在Redux中，我们把这种结构固定的对象取个名字，就叫 action对象
- 同一种行为不太可能只触发一次，所以这才有了action创建函数。

直接创建

`````React
var addTodo=function(text){
    return{
        type:'add_todo',
        text:text
}
}

//调用：
store.dispatch(addTodo('睡觉'));
`````

### Reducer

**初始化状态，加工状态**

Recuder函数最重要的特征是，他是一个纯函数。也就是说，只要同样的输入，必定得到同样的输出。

Recuder指定了应用状态的变化如何响应action并发送到store的，记住actions只是描述了有事情发生了这一个事实，并没有描述应用如何更新state。

reducer是哟个函数，他接受action和当前的state作为参数，返回一个新的state。

````React
var initdata=['乐器'];
var reducer=function(state=initdata,action){
    switch(action.type){
            case 'add_todo';
            return[...state,...action.text]
            default:
            return state;
    }
}
````

纯函数是函数式编程的概念，必须遵守以下约束

- 不得改写参数（不能改变state）
- 不能调用系统I/O的API
- ·不能调用Date.now()或者Math.random()等不纯的方法，因为每次会得到不一样的结果
- Reducer函数里面不能改变State，必须返回一个全新的对象，请参考下面的写法，因为每次会得到不一样的结果。
- reducer函数里面不能改变state，必须返回一个全新的对象。

### store

**store是用来维持应用所有state树的一个对象。**改变state的唯一方法是store dispatch一个action。

store不是类，而是一个有几个方法的对象，可以采用createStore进行创建。

createStore(reducer,[initState, enhancer])

作用:创建一个Redux store来存放应用中所有的state，一个应用只能有个store。函数返回store对象。

参数:

 reducer(Function):两个参数: state和action，返回一个state。不要对参数state进行修改，需要返回一个新的对象

initStatate:初始state。如果不为空，需要和reducer中处理的state结构一致= enhancer:—个中间件,如logger等。

方法：

- getState()：返回应用当前的state树，他与store的最后一个reducer返回值相同
- dispatch(action)：分发action，这里是改变state的唯一方法。
- subscribe(listener)：添加一个变化监听器，每当dispatch action的时候都会执行，state树中的一部分可能已经变化。你可以在回电函数中调用getState()来拿到当前state。函数返回一个解绑的函数。

`````React
import React from "react";
import { createStore } from "redux";

let add_action = function (value) {  //调用方法者
  return {
    type: "add",
    data: value,
  }
}
let del_action =function(index){
  return{
    type:'del',
    data:index,
  }
}

function reducer(prestate, action) {  //事件处理者
  switch (action.type) {
    case "add":
      return { "goods": [...prestate.goods, action.data] }//怎么捕捉这个对象？    返回给了store，覆盖了之前的数据
      break;
    case "del":
      let newarry={'goods':[...prestate.goods]}  //重新赋值新数组
      newarry.goods.splice(action.data,1);   //切除不要的元素
      return {"goods":newarry.goods};  //返回对象
      break;
    default: return prestate
  }
}

let object_state = { "goods": ["牛奶", "苹果"] }  //定义变量存储数据
let Store = createStore(reducer, object_state)  //定义仓库，将定义中的数据存入其中    


class AppTT extends React.Component {
  constructor() {
    super()
    this.state = { "good": Store.getState().goods } //读取数据，显示初始数据
  }
  
  render() {
    let g;
    g = this.state.good.map( (value, index)=> {   //遍历状态中的数据，放在li中
      return <li key={index}>{value} <button dataindex={index}>delete</button></li>
    })
    return <div>
      <p>
        <input type="text" ref="g" /><button onClick={this.addGoods}>添加</button>
      </p>
      <ul onClick={this.delGoods} >{g}</ul>
    </div>
  }
  addGoods = () => {
    Store.dispatch( (this.refs.g.value)); //分发action，把input中的数据放入action中。
  }
  delGoods=(e)=>{
    if(e.target.nodeName=='BUTTON'){
      let index=e.target.getAttribute('dataindex');     //获取当前的index值
      Store.dispatch(del_action(index));   //分发action，把要删除的数据的index放在action。
    }
  }
  componentDidMount() {
    Store.subscribe(() => {  // 监听，store中的数据是否发生了变化
      this.setState({ "good": Store.getState().goods }) //将变化了数据放在状态中
    })
  }
}
export default AppTT;
`````

## 异步action和中间组件

### 异步action

同步action就是指，返回值是一个对象类型的一般对象

`````react
export const asyncAction = (data,time) => {
    return { 
        type:'',
        data:''
    }
}
`````

**所谓异步action就是指，action的返回值是一个函数，而不是一个对象（需要中间件），异步中都会调用同步action，异步action不一定是必要的（非必须）**

````react
export const asyncAction = (data,time) => {
    return ()=>{
        setTimeout(()=>{
            store.dispatch({type:'+',data})  //需要中间件，让redux可以处理中间件，处理之后函数体内容，重新与store对话，将要传递的type和data传出。
        },time)
    }
}
````

### 中间件

#### redux-thunk

````react
npm i redux --save-dev         安装
````

```react
import thunk from 'redux-thunk'  //引入
import {createStore,applyMiddleware} from 'redux'  //执行中间件


//stroe中
export default createStore(countReducer,applymiddleware(thunk))  //作为第二个参数
```

### React-readux介绍和原理

React和Redux事实上是两个独立的产品，可以使用React而不是使用Redux，也可是使用Redux而不是React，而是一个名叫react-redux的库是将react和redux结合的一个库；通过redux api的封装形成基于react的组件，操作更加简洁。

分为**容器组件**和**UI组件**

- 所有UI组件都应该包裹一个容器组件，他们是父子关系
- 容器组件是真正和redux打交道的，里面他们可以随意使用redux的api    
- UI组件中不能使用任何redux的api
- 容器组件会传给UI组件：（1）。redux中所保存的状态。（2）。用于操作状态的方法。
- 备注：容器给UI传递：**状态、操作redux中的状态的方法，均通过props传递，主要目的是实现UI组件和容器的分离**。

![mark](http://qiniu.cloud-zhi.com/blog/210421/38je8HB37a.png?imageslim)

#### 安装

````js
npm i redux --save-dev   //必须要先安装redux
````

`````js
npm i react-redux --save-dev  //安装react-redux
`````

#### 原理

最主要的功能：

- connect：链接数据处理组件和内部UI组件；
- Provider：提供包含store的context；把我们用redux创建的store传递到内部的其他组件。让内部组件可以享有这个store并提供对state的更新。

通过connect实现传递store的目的

provider组件最主要是用于UI组件，并且将store传递到内部其他子组件当中，connect方法的主要作用是链接数据处理组件和ui组件，connect方法通过三个主要的参数，这三个参数是三个函数，主要的作用利用redux api实现对store的操作；从而更新state重新渲染UI组件。

#### provider组件

想要把store绑定在视图上，得到React-redux中两个主角provider和connect，通常情况下你无法使用connect()去connect一个没有继承provider的组件，也就是说如果你想在某个组件中使用redux维护的store数据，他必须是包裹在provider中并且被connect过得组件，**provider的作用类似于提供一个大容器，将组件和redux进行关联，在这个基础上，connect在进行store的传递，需要引入store**

````React 
<Provider store={store}>  //通过props将唯一的store传递给子组件
      <Router history={history}>
            <Route path='/' component={App}>
                    <Route path='foo' component={Foo}></Route>
                    <Route path='bar' component={Bar}></Route>
             </Route>
    </Router>
</Provider>
````

#### connect方法

connenct并不会改变它连接的组件，而是提供一个经过包裹的connect组件，将store和组件联系起来。

`````react
export default connect([mapStateToProps], [mapDispatchToProps], [mergeProps],[options])(className)
`````

conenct接受4个参数，分别是mapStateToProps，mapDispatchToProps，mergeProps，options

- mapStateToProps(state)方法允许我们将store中的数据作为props绑定到组件中，只要store更新了就会调用mapStateToProps方法,mapStateToProps返回的结果必须是object对象，该对象中的值将会更新到组件中

  **1、mapStateToProps函数返回是一个对象；**

  **2、返回的对象中的key就作为传递给UI组件props的key，value就作为UI组件props的value；**

  **3、mapStateToProps用于传递状态。**

- mapDispatchToProps(dispatch,[ownProps])传入dispatch，第二个参数允许我们将action作为props绑定到组件中，mapDispatchToProps希望你返回包含对应action的object对象。

  **1、mapDispatchToProps函数返回是一个对象；**

  **2、返回的对象中的key就作为传递给UI组件props的key，value就作为UI组件props的value；**

  **3、mapDispatchToProps用于传递操作状态方法。**

- mergeProps: mergeProps如果不指定，则默认返回Object.assign(0, ownProps, statePropsdispatchProps)，顾名思义，mergeProps是合并的意思，将state合并后传递给组件。

- options：通过配置项可以更加详细的定义connect的行为，通常只需要执行默认值。

````React
function mapStateToProps(state)(//函数返回对象中的key就作为传递给UI组件props的key值，value就作为传递给props的value
    return {n:state}
}

//函数返回对象中的key就作为传递给UI组件props的key值，value就作为传递给props的value——操作状态的方法 
 function mapDispatchToProps(dispatch){
     return {add: function (value) { dispatch({ type: 'add', data: { id: num++, name: value, isDidIt: false } }) },
                del: function (id) { dispatch({ type: 'del', data: id }) },
                clean:(id) => {
                   dispatch({type:'clean',data:id}) 
                }} 
}
"export default connect(mapStateToProps,mapDispatchToProps)(TodoApp)

````



