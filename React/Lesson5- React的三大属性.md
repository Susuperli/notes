# React的三大属性

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
this.setState({'data':data},[callback]) //callback会在render之后调用，即可以得到异步结果
`````

![mark](http://qiniu.cloud-zhi.com/blog/210421/8FA4j6BEA7.png?imageslim)

这是一个React组件实现组件可交互所需的流程，render()输出虚拟DOM，虚拟DOM转化为真实DOM，再在DOM上面注册事件，事件触发setState()修改数据，在每次调用setState方法时，React会自动执行render方法来更新虚拟DOM，如果组件已经被渲染，那么还会更新到DOM中去。

另外还有函数式的setState方法

````react
this.setState((state,props)=>{
    return {count:count+1}
})
````

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

### refs属性

#### refs和DOM

在常规的React数据流中，props是父组件与子组件交互的唯一方式。要修改子元素，你需要用新的props去渲染子元素。然而，在少数情况下，你需要常规数据流来强制修改子元素。被修改的子元素可以是Reat组件实例，或者是一个DOM元素。在这种情况下，React提供解决办法：使用Refs

**refs是组件实例对象中的一个属性，值是一个对象，只需要给vdom添加ref属性即可生成ref的指向，指向该dom，类似于原生js中通过id获取节点。**

#### 常见形式

- 字符串形式的ref
- 回调函数的ref
- createRef()创建ref

#### 应用场景

- 处理focus、文本选择或者媒体播放
- 触发强制动画
- 集成第三方DOM库

注：

>如果可以通过声名式实现，就尽量避免使用refs。
>
>你可能首先会想到在你的应用程序中使用refs来更新组件。如果是这种情况，请花一点儿时间，更多的关注组件中使用state。在组件层中，通过较高界别的state更为清晰。

#### 字符串形式的ref

````React
<input ref="myinput"></input>//创建

this.refs.myinput  //访问
````

#### 回调函数

refs属性的值除了是一个字符串，还可以是一个函数，这个函数是一个回调函数，在组建初始化或者更新的时候由React调用，这个回调函数会得到一个参数，即当前的节点对象，我们可以将得到的节点对象挂在组件的实例对象上，在需要的地方调用

`````React
class Refs extends React.Component{
       render(<div>
        <input type="password" ref={(element)=>{this.setTextInput=element}} onBlur={this.showData}></input>//创建
    </div>)
    
     showData=()=>{  //调用
        const inputs=this.setTextInput;
        console.log(inputs)
    }
}
`````

#### createRef

`````React
class CreateRef extends React.Component{
    constructor(){
        super();
        this.name=React.createRef();  //创建
        this.pwd=React.createRef();
        this.nav=React.createRef();
    }
    render(){
        return(<div>
            <p>用户名：<input type="text" ref={this.name}></input></p>
            <p>密码：<input type="password" ref={this.pwd}></input></p>
            <button onClick={this.getFormData}>登录</button>
            <Dom ref={this.nav}></Dom>
        </div>)
    }
    getFormData=()=>{
        let name=this.name.current;
        let pwd=this.pwd.current;
        console.log(this.nav.current)
    }
}
`````





