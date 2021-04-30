# 第八讲 路由

## 单页面应用程序（SPA）

单页面web应用（single page web application）

- **整个应用只有一个完整的页面**。
- 点击页面的链接**不会刷新**页面，只会做页面的**局部更新**。
- **数据都需要通过ajax请求获取，并在前端异步表现**

### 理解路由

多页面网站是通过超链接来实现页面的切换的，所有每次点击超链接时浏览器都需要刷新请求新的页面，而单页面应用程序主要通过路由来实现内容的切换,在react当中也就是切换组件，那如何实现组件的切换呢?**react路由是通过一种特殊的链接，点击时会修改浏览器地址栏中的地址**，但是浏览器是会忽略掉这次变化所有切面不会被跳转，但是在路由会监听到地址（path）的变化从而根据不同的地址渲染出来不同的组件(component)

**一个路由就是一个映射关系（key:value）**

key为路径，value可能是function或是component。

### 简介

- 目前，官方同时维护2.x和4.x两个版本，React16以上只支持router4.x版本
- react Router4.0（以下简称RR4）它遵循React的设计理念，即万物皆组件。所以RR4只是一堆提供了导航功能的组件（还有若干对象和方法），具有声名式（引入即用），可组合性特点。

### 安装

react-router-dom --save-dev

### 路由器组件

\<Router>

如果我们希望页面中某个部分内容需要根据URl来动态显示，需要用到Render组件，该组件是一个容器组件，只需要用它包裹URL对应的根组件即可。

Router是所有路由器组件公用的底层接口，一般我们的应用并不会使用这个接口。而是使用高级的路由：

**\<BrowserRouter>：使用HTML5提供了的history API来保持UI和URL的同步；**

**\<HashRouter>：使用URL的hash（例如：window.local.hash）来保持URL和UI的同步；**

\<MemoryRouter>：能在内存保存你“url”的历史记录（并没有对地址栏读写）；

\<StaticRouter>：从来不会改变历史。

**注：这里\<Router>组件下只允许存在一个子元素，如存在多个则会报错。**

### 路由匹配组件

\<Route>

主要作用是当一个location匹配路由的path时，渲染某些UI。

Route组件的主要作用就是当一个location匹配的路由器的path，渲染某些UI

path（string）：路由匹配路径

exact（bool）：exact属性表示路由器使用精确的匹配模式，非exact模式下/匹配所有的/开头的路由器，一般都会设置，值可以省略。

component：设置要显示的组件，该属性以props的方式传入。

### 导航组件

\<Link>

用来处理a链接类式的功能（他会在页面中生成一个a标签），但设置这里需要注意的，react-router-dom拦截了实际的默认动作，然后根据所有使用的路由模式（hash或者HTML5）来进行处理，改变了URL，但是不会发生请求，同时route中的设置把对应的组件显示在指定位置。

to（string/object）：要跳转的路径或者地址。

replace：为true时，点击链接后将使用新地址替换掉访问记录的原地址；为false时，点击链接后将在原有访问历史记录的基础上添加一个新的记录。默认为false。

\<NavLink>

activeClassName

active

\<Switch>

该组件只是渲染首个被匹配的组件

### **路由重定向**

引入Redirect组件

````React
import { Link, BrowserRouter, Route ,Redirect} from 'react-router-dom';


<Redirect to='/home'></Redirect> //直接指向默认的路径，上来的时候直接渲染这个路径。
````

### 路由传参

#### 通配符传值params

传递：

`````React
  <BrowserRouter>
            <Link to={`/about/我是摇摆羊`}>About</Link>  //传递者，通过/+传递的内容
    
    
            <Route path='/about/:name' component={About}></Route>  //接受者，通过/:+定义的变量。
 </BrowserRouter>
`````

接收：

````react
this.props  //可通过props接收  Object
                    //history: {length: 2, action: "PUSH", location: {…}, createHref: ƒ, push: ƒ, …}
                    //location: {pathname: "/about/我是摇摆羊", search: "", hash: "", state: undefined, key: "2t7e0a"}
                    //match:
                    //isExact: true
                    //params: {name: "我是摇摆羊"}
                    //path: "/about/:name"
                    //url: "/about/我是摇摆羊"
                    //__proto__: Object
                    //staticContext: undefined
                   // __proto__: Object

this.props.match.params         //{name: "我是摇摆羊"}
````

#### 通过query传参

`````react
{/* search方式 */}
                    <Link to={`/about/?id=1&name=吕泽准`}>About</Link>

 {/* search方式声明 ,无需声明*/}
                    <Route path='/about' component={About}></Route>
`````

`````react
import qs from 'querystring'  //引入jQuery库，用来直接切割字符创

this.props.location.search   //?id=1&name=吕泽准
const {id,name}=qs.parse(search.slice(1))  //1 吕泽准
`````

#### 通过state传值

```react
{/* state方式 */}
                    <Link to={{pathname:'about',state:{id:233,name:'我叫眯眯眼'}}}>About</Link>

{/* state方式声明 ,无需声明*/}
                    <Route path='/about' component={About}></Route>
```

`````React
console.log(this.props.location.state) //{id: 233, name: "我叫眯眯眼"}
`````

**该方法地址栏路径没有改变（其他方法都会），刷新也不会丢失**

### withRuter

```react
import {withRouter} from 'react-router-dom'   //允许你在一般组件中使用路由组件的API

export default withRouter(xxxx)  //返回值是一个新组件
```

## BrowserRouter和HashRouter的区别

![mark](http://qiniu.cloud-zhi.com/blog/210421/CA1LhEab54.png?imageslim)

## lazyload

其实路由是会加载所有组件，当组件较多时我们只希望加载想要的就可以用lazyload，

引入lazyload

````react
import React, {Component,lazy} from 'react'
````

使用引入路径

````react
const Home=lazy(()=> import('./Home'))
````

引入\<Suspense fallback>.....\</Suspense>

`````react
<Suspense fallback={<h1>加载中</h1>}>
    注册路由
    <Router path='aboue' component={}></Router>
    <Router></Router>
</Suspense>

`````

