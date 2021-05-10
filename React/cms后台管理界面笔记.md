#  cms后台管理界面笔记

## 准备工作

- 搭建环境
- 建立所需文件夹，如api完成前后台数据交互，主要是来接受来自后台的数据、page主要是路由组件、component主要是一般组件、utils完成一般的工具和assets
- 使用git存储在GitHub上

## 登陆界面的完成

### antd

引入antd，主要是对form表单应用，来验证从浏览器或得的用户名和密码，使用其自带的验证功能完成验证。

### api

利用axios对自己ajax进行封装

`````jsx
// 能发送异步ajax请求的函数模块
// 封装axios库
// 函数返回值是一个promise对象
/*
1、优化：统一处理请求异常
   在外层包一个自己创建的promise对象
   在请求出错时，不去reject（error），而是现实错误提示。
2、优化2：异步得到不是response而是response.data
   在请求成功resolve时，resolve(response.data)
*/

import axios from 'axios'
import {message} from 'antd'

export default function ajax(url,data={},method='GET') {

    return new Promise((resolve,reject)=>{
        let promise;
        //1、异步ajax请求
        if(method==='GET') {  //发送GET请求
            promise=axios.get(url,{  //配置对象
                params: data //指定请求参数
            })
        } else {  //POST请求
            promise=axios.post(url,data)
        }
        //2、成功，调用resolve(value)
        promise.then(response => {
            resolve(response.data)
        //3、失败了，不调用reject(reason)，而是提示异常信息
        }).catch(error => {
            //reject(error)
            message.error('请求出错了'+ error.message)
        })
    })
}
`````

axios获得的数据是一个promise对象，即可以利用then和catch方法，对得到的数据进行处理。方便调用

### 路由的建立

app组件中使用浏览器路由器

`````react
    <BrowserRouter>
    <Switch>{/*只匹配其中一个*/}
    <Route path='/login' component={Login}></Route>
       <Route path='/' component={Admin}></Route>
    </Switch>
    </BrowserRouter>
`````

### 登陆

主要是对后台返回数据的验证，根据返回的状态判定返回的数据是否正确，若正确则是会返回到管理界面，这里用到的是props中的history属性

login.jsx

1、调用登陆接口请求

2、如果失败，显示错误信息

3、如果成功了，保存user到local中

​      跳转到admin

````js
this.props.history.replace('/')
````

4、如果内存中有user的值，自动跳转到admin

src/index.js

​     读取local中user到内存中保存

admin.jsx

判读内存中没有user（_id没有值），自动跳转到local

### 数据管理

在utils中建立新的组件来储存用户登陆的信息，这里使用了store的库（原理还是localStorage）来帮助管理信息。

`````jsx
/*
存储本地数据来实现登录状态的维护，即登陆之后，刷新界面并不会返回登录界面。
这里引入插件store
*/
import store from 'store'

const USER_KEY = 'user_key';
export default {
    // 添加
    saveUser(user) {
        store.set(USER_KEY, user)
    },
    // 读取
    getUser() {
        return store.get(USER_KEY) || {}
    },
    // 删除
    removeUser() {
        store.remove(USER_KEY)
    }
}
`````

### 登陆状态的维护

主要是通过是否存在用户信息来进行页面的选择，在store中是否有用户信息。如有保持在管理界面，没有，则保持在登录状态。实现则是通过路由的重定向。当然，这个判定是通过index.js中进行的，这样无论是页面刷新或是重新打开浏览器都是优先判断是否存在用户信息，利于展示。

index.js

`````js
// 获取来自local值，判断是否登录
const user=stroageUtils.getUser();
memoryUtils.user=user;

`````

判定（render和方法中的跳转方式不一样）

````jsx
    render() {
        //判断用户是否登陆,如果登录自动跳转到管理界面，且维持在管理界面。
        const user=memoryUtils.user
        if(user && user._id){
           return <Redirect to='/'></Redirect>
        }
    }
````

````jsx
    render() {
        const user=memoryUtils.user;
        //如果没有user ==> 即没有登录
        if(!user || !user._id){
            //自动跳转到登陆（在render()中）
            return <Redirect to='/login' /> //使用路由的重定向，指向登陆界面
        }
    }
````

## 整体界面的搭建

整个cms的管理界面的‘厂’字型的结构是基于antd的layout布局

### 使用leftnav组件

1、使用antd menu/item/submenu

2、使用react-router

​      withRouter()包装：包装费路由组件，给其传入history、location、match属性

3、componentWillMount和componentDidMount的比较

​     will在第一次的render前调用一次，为第一次render准备数据（同步）

​     did在render之后调用一次，启动异步任务，后面状态的更新

4、根据动态生成Item和submenu的数组

​     map（）+递归：多级菜单列表

​     reduce（）+递归：多级菜单列表

`````jsx
getMenuNodes = (menuList) => {
        const path=this.props.location.pathname; 
        return menuList.map((item) => {
            if (!item.children) {
                return (<Menu.Item key={item.key} icon={item.icon}>
                    <Link to={item.key}>
                        {item.title}
                </Link>
                </Menu.Item>)
            }else{
                //有二级菜单的需要判断被默认选中的时候需要展开，不然到时候观察不到默认选中的位置
                //查找一个与当前路径匹配的自item
                const cItem=item.children.find(cItem => cItem.key===path)
                if(cItem){//如果存在就说明，当前item所对应的子列表需要展开
                this.openKey = item.key  //帮当前的key存入一个变量中
                }
                return(<SubMenu key={item.key}  title={item.title} icon={item.icon }>  
                    {this.getMenuNodes(item.children)}   {/*在这里使用递归，继续调用该方法*/}
                </SubMenu>)
            }
        })
    }
`````

5、两个问题

   刷新是如何选中对用应的菜单项？

​       selected是对应当前请求的path

   刷新子菜单路径时，自动打开子项目列表

​      openkey是一级列表项的某个子菜单项是当前对用的菜单项，主要是对antd组件api的熟悉程度。

## 页面功能完善

页面路由的搭建，建立由各个项目列表所对应的子路由界面。实现点击的跳转

`````jsx
                        <Switch>
                            <Home path='/home' component={Home}/>
                            <Category path='/category' component={Category}/>
                            <Product path='/product' component={Product}/>
                            <Role path='/role' component={Role}/>
                            <User path='/user' component={User}/>
                            <Bar path='/bar' component={Bar}/>
                            <Line path='/line' component={Line}/>
                            <Pie path='/pie' component={Pie}/>
                            <Redirect to='/home'/>
                        </Switch>
`````

默认时指向home界面，通过路由的重定向功能实现。

## header页面的构建

![mark](http://qiniu.cloud-zhi.com/blog/210503/0Ab7JFcEec.png?imageslim)



主要功能包括，显示登录界面、显示登录user名称、显示天气、显示时间、退出登录

### 获取时间

获取时间的功能是new一个时间对象，通过一个小插件来实现时间显示的标准化。然后通过setInterval循环定时器来实现时间的更新，通过setState来实现页面的刷新。

### 获取天气

天气的功能是借用了高德地图提供的api接口，首先使用太平洋的接口来获取时时的citycode，提供给高德的api，通过简单的分割来实现动态的显示。太平洋接口需要代理，如下显示。

#### jsonp跨域的复习

  我们可以利用src属性可以没有同源限制的原理来解决ajax跨域问题

- jsonp只能解决GET类型的ajax请求跨域问题。

- jonp请求不是ajax请求，而是一般的get请求。

  基本原理

- 浏览器端

​        动态生成\<script>来请求后台接口(src的接口的url)

​        定义好的用于接收响应数据的函数fn，并将函数名通过请求的参数提交给后台，如：callback=fn。

-  服务器端

​         接收到请求处理产生的结果数据后，返回一个函数的调用的js代码，并将结果数据作为实参传入函数调用

- 浏览器端

​        收到响应的自动执行函数调用的js代码，也就执行了提前定义好的回调函数，并得到了需要的结果数据。

#### 多网址代理的实现

一个项目中如果需要使用代理多次网址，可以使用react提供的多代理服务。

**简介代理**：一般网页想要请求别的服务器的内容，因为同源策略的存在，会导致跨域并不能成功，而代理服务器就可以帮助我们完成跨域的请求。跨域是对于客户端和服务器来说的，而对于服务器和服务器之间是没有跨域一说，代理服务器就是扮演这样一个“中间人”地服务。

 \* **突破自身IP访问限制：**访问国外站点或者其他之前不能访问的站点。
 \* **提高访问速度**：通常代理服务器都设置了一个较大的硬盘缓冲区，当有外界的信息通过的时候，同时也将其保存在缓冲区中，当其他用户在访问相同的信息时，则直接有缓冲区取出信息，传给用户，以提高访问速度
 \* **链接内网与Internet，充当防火墙**：因为所有的内部网用户通过代理服务器访问外界时，只映射一个IP地址，所以外界不能直接访问到内部网；同时可以设置IP地址过滤，限制内部网对外部的访问权限
 \* **隐藏真实IP**：上网者可以通过这种方式隐藏自己的IP，以免受到攻击；
 \* **设置用户验证和记账功能，没有登记的用户无权通过代理服务器访问Internet网**。并对用户的访问时间、访问地点、信息流量进行统计。

在src根目录建立Proxy用的js文件来实现多网址代理的设置。配置如下

安装

`````js
npm install http-proxy-middleware --save-dev
`````

````js
const {
  createProxyMiddleware
} = require('http-proxy-middleware');

module.exports = function (app) {
  app.use(
    createProxyMiddleware("/api", {    //第一个参数为当网站在请求数据的时候碰到的关键字；第二个参数为一个对象是关于此次的配置
      target: "http://whois.pconline.com.cn",  //代理网址
      changeOrigin: true,
      ws: true,
      pathRewrite: {   //碰到以api开头的网址，将api变成空字符串，代理网站代替api。
        '^/api': ''
      }
    })
  );
};
````

````js
export const reqCity = () => ajax('/api/ipJson.jsp?json=true');
````

#### 退出功能的实现

退出的实现比较简单，总的来说就是实现了一个页面的跳转以及删除我们存储在变量中的登录信息。

UI显示借用了antd的modal组件，点击弹出对话框，当点击确认之后。**先删除用户信息**，注意这里一定要先把用户信息删除，然后再跳转到login页面。否则会形成在两个页面的反复横跳而导致的报错。

## 商品管理界面

### 品类管理

#### 数据的获取显示

整体页面的构建主要是借用了antd所提供的Card、Table组件。

![mark](http://qiniu.cloud-zhi.com/blog/210506/FcD1DEkhKL.png?imageslim)

大体思路如下：该列表的显示都是由一个接口实现，分为一级列表，每个一级列表都有其子分类。请求不同的数据时向接口传递不同的参数。一级列表的参数是0，返回的字段中包含一级列表的内容和一个\_id值，该值可以作为请求其子分类的参数，该值作为子分类的parentId，同一分类的所有子类共享一个parentId，每个子类也有一个代表自己的\_id值。

##### async的封装

​        async对于处理异步请求有其优异的封装性，对将要进行的ajax请求前使用await关键字，可以使要进行的异步操作实现同步的视觉感受，await会进行等待，直到ajax得到结果，并且会对得到promise对象自动使用then()方法，取到正确的结果（这里只会使用then方法，而没有catch方法）。将得到的结果赋给一个变量，对变量进行操作即可。

浅谈await等待

await等待的是谁：如果它等到的**不是一个 Promise 对象**，那 await 表达式的运算结果就是它等到的东西。

如果它等到的**是一个 Promise 对象**，await就会**阻塞**后面的代码，等着 Promise 对象 resolve，然后得到 resolve 的值，作为 await 表达式的运算结果。

##### 对于async封装下this.setState()表现的探究

`````jsx
getCategorys = async () => {
        console.log('进入async函数')
        console.log('显示前')
        this.setState({ loading: true })  // 显示loading
        console.log('显示后')
        const { parentId } = this.state
        const result = await reqCategorys(parentId);  //请求分类状态
        console.log('隐藏前')
        this.setState({ loading: false })   //隐藏loading
        console.log('隐藏后')
        if (result.status === 0) {
            //取出分类列表可能是一级的也可能是二级的
            const categorys = result.data;
            if (parentId === '0') {
                this.setState({ categorys }); //更新一级分类状态
            } else {
                this.setState({ subCategorys: categorys }); //更新二级分类状态
            }
        } else {
            message.error('获取分类列表失败')
        }
    }
`````

![mark](http://qiniu.cloud-zhi.com/blog/210506/j6Ec2JEk11.png?imageslim)

在setState()前后分别表现为异步和同步，在await之前变现为异步，在await之后表现为同步。

##### setState()的渲染机制

setState()在大多数情况下表现为“异步”，其实setState()的异步是react机制，其实是状态不会立即执行。为了优化性能react会将所有setState()放在最后一块渲染，用来避免重复渲染带来的内存浪费。

> `setState()`方法通过一个队列机制实现`state`更新，当执行`setState()`的时候，会将需要更新的`state`合并之后放入状态队列，而不会立即更新`this.state`(可以和浏览器的事件队列类比)。如果我们不使用`setState`而是使用`this.state.key`来修改，将不会触发组件的`re-render`。如果将`this.state`赋值给一个新的对象引用，那么其他不在对象上的`state`将不会被放入状态队列中，当下次调用`setState()`并对状态队列进行合并时，直接造成了`state`丢失。

 同样setState()在部分情况下也会表现为同步，即在一个异步操作中，例如定时器中，或者await（后面是一个promise对象）后面，都会变现为同步；以及setState()方法所提供的的第二个参数，一个回调函数，在里面可以得到同步的状态值。

#### 数据的修改

#### 数据的添加

### 商品管理



