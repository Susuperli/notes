# 第四讲 组件

React推出后，出于不同的原因先后出现两种定义react组件的方法。

## 函数式组件

他是为了创建展示组件（简单组件），这种组件只负责根据传入的props（属性）来展示，不涉及到要state状态的操作。具体的无状态函数式组件

在大部分React代码中，大多数组件被写成无状态的组件，通股票简单的组合可以构建成其他组件等；这种通过多个简单然后合并成一个大应用的设计模式被提倡。

````react
import React from 'react';
function NewList(){
    return (<ul>
        <li>新闻</li>
        <li>新闻</li>
        <li>新闻</li>
        <li>新闻</li>
        <li>新闻</li>
    </ul>)
}
export default NewList;
````

**函数式组件**

在调用ReactDOM.render()之后发生了什么？

React解析组件标签，找到组件，发现组件是函数定义的，随后调用函数，将返回的虚拟dom转换成真实的dom，随后呈现在页面中。

**特点**

- 组件不能访问this对象

- 组件无法访问生命周期的方法
- 无法访问state状态，只能访问输入的props，同样的props会得到同样的渲染结果，不会有副作用。

**为什么不能访问this**

函数由react调用，调用过程中，babel转换器将jsx转化为js，这时函数会自动开启严格模式，严格模式中规定全局模式下自定义的函数中this不能指向window，所以this的结果是undefined。

## 类式组件

`````React
class Nav extends React.Component {
    constructor(){
        super();
    }
    render(){
        console.log(this)
        return <div>
            <button onClick={this.login}>click me</button>
        </div>
    }
    login=()=>{  //箭头函数改变this指向
        console.log(this);
        alert('请登录')
    }
}
`````

### 注意

- 使用类创建组件，必须继承react内置的一个组件React.Component。
- constructor()方法，可以省略
- 必须要有render()方法，用于生成虚拟dom，该方法被定义在类的原型上，供实例使用。

**类式组件**

在调用ReactDOM.render()之后发生了什么？

React解析组件标签，找到组件，发现组件是类定义的，随后new出来一个该类的实例，并调用这个实例上面的render方法，将返回的虚拟dom转换成真实的dom，随后呈现在页面中。

由于render方法是有该类实例调用的，所以render中的this，指向的是由类创建的实例对象即组件实例对象。

 **React类组件中自定义的方法函数中this丢失的问题?**

正常情况下方法中的this是指向调用该方法的实例对象，但是在react中调用该方法是并没有直接调用，例如this.handleClick(),而是以参数的形式将该方法函数传入，作为回调函数由react直接调用,同时又因为类中的方法在定义时默认开启了局部的严格模式，导致this不能执行window，所以this为undefined导致丢失

## React组件对象的三大属性

- 控制组件更新的state。
- 负责传值的props。
- 存储当前节点的refs。

### state状态

组件免不了用户互动，React的一大创新就是将组建看成一个状态机，一开始有一个初始的状态，然后用户互动，从而触发新的UI。

React中，只需要更新组建的state，然后更具新的state重新渲染用户界面（不要操作dom）。

**state在哪？**

state是在组件的实例对象中的，组件是实例对象是有类生成的所以只有类式组建中才有state。

#### **如何初始化state**

state是组件实例对象继承自React.Component的，所以要在当前组件的构造器中进行初始化，默认值为null

`````React
class MyComponent extends React.Component{
    constructor(prop){
        super(prop);
        this.state={
            key:value
        }
    }
}
`````

### state的工作原理

#### 修改方法

常用的是方法是调用setState(date,callback),这个方法会合并data到this.state，并且重新渲染组件，渲染完成后，调用可选的callback回调，大部分情况下不需要提供callback，因为react会负责把界面更新到最新状态。

特点

- 组件状态改变时，可以通过this.setState修改状态
- 仅当setState传入的对象包含字段可以才会修改属性
- 每次调用setState会导致重新渲染调用render方法
- 直接修改state不会导致重渲染组件

`````React
this.setState({'data':data})
`````

![mark](http://qiniu.cloud-zhi.com/blog/210421/73iBCGiH0j.png?imageslim)

这是一个React组件实现组件可交互所需的流程，render()输出虚拟DOM，虚拟DOM转化为真实DOM，再在DOM上面注册事件，事件触发setState()修改数据，在每次调用setState方法时，React会自动执行render方法来更新虚拟DOM，如果组件已经被渲染，那么还会更新到DOM中去。

#### 简写方法

在类中直接写赋值语句。

`````React
class MyComponent extends React.Component{
    state={'ishot':true};
render(){
    return(<h1>{this.stste.ishot}</h1>)
}
}
`````

如果事件的处理函数绑定实例通过箭头函数的方式，则构造器完全可以省略不写。

### React props

props相对于组件来说就是外来属性，使用props可以从组件外部向组件内部传值，类似函数的传参，经常用于组件之间的传值，一种父级向子级传递数据的方式。

父向子传值直接使用props即可

`````React
// 类式传参
class Nav extends React.Component {
    constructor(){
        super();
    }
    render(){
        return <div>
            <Dom aa={this.props.ff}></Dom> //传值方式
        </div>
    }
}
`````

````React
class Dom extends React.Component{
    constructor(){
        super()
    }
    render(){
        return(<div>
            <h1> <span>from kk </span> {this.props.aa}</h1> /*接收方式*/
        </div>
    }
}
````

#### **子向父传值** 

先在父组件中定义一个函数用于接收子组件传过来的值，然后使用props将该函数传递到子组件中，最后在子组件中调用该函数同时传参。

父组件

`````React
class App extends React.Component{
    constructor(){
        super();
        this.state={
            'data':'a'
        }
    }
    render(){
        return (<div>
            <h1>fromfather {this.state.data}</h1>
            <Nav fn={this.getNav}></Nav>  {/*构建回调函数，并将函数传递给子组件*/}
        </div>)
    }
    getNav=(data)=>{
        console.log(data)
        this.setState({'data':data})
    }
}
`````

子组件

````React
class Nav extends React.Component {
    constructor(){
        super();
        this.state={ //设置状态
            'x':'你好',
            'data':'wo'
        }
    }
    render(){
        return <div>
            <div><span>from son  </span>  {this.state.data}</div>
            <button onClick={this.changeState}>clickMeToChange</button>{/*点击触发事件*/}
        </div>
    }
    changeState=()=>{  //箭头函数改变this指向
        this.setState({'x':'lily'}) //修改状态,setState()是异步的方法，故第一次输出是'你好'；后才是'lily'。
        this.props.fn(this.state.data) //利用props属性调用传递的回调函数，并将子向父要传递的数据作为参数。
    }
}
````

#### **同父兄弟中**

子向父传，父向另子传。两步结合不做赘述。

#### React中state和props的区别

React中数据流是单向的，只会从父组件传递到子组件。属性

props（properties）是父组件向子组件状态传递的接口，React会向下遍历整个组件树，并且重新渲染使用这个属性的组件。

props可以理解为父组件与子组件的状态传递，而React的组件都有自己的状态，这个内部使用state表示，state只能在组件内部使用，state只应该储存简单的视图状。

state是可以通过setState修改，而props是只读的。

#### 本地图片加载问题

````React
render(){
    return <div>
        <img src={require('path').default}/>
    </div>
}
````

也可

````React
import img from 'path'

render(){
    return <img src={img}></img>
}
````





