# cms后台管理界面笔记

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

5、两个问题

   刷新是如何选中对用应的菜单项？

​       selected是对应当前请求的path

   刷新子菜单路径时，自动打开子项目列表

​      openkey是一级列表项的某个子菜单项是当前对用的菜单项

## 页面功能完善



