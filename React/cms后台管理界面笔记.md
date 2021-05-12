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

数据的修改和添加所使用的界面是基于antd的model弹框，当点击事件触发时就会利用state来控制弹框的显示进和隐藏。![mark](http://qiniu.cloud-zhi.com/blog/210511/0e5HG19gg3.png?imageslim)

主要是利用form表单从获取值，并将信息传递给父组件。本例中利用的是antd中的form组件，antd4.x与3.x的改动较大，4.x版本获取表单信息的过程如下。

​      通过ref属性绑定from表单，以此来获取form表单的信息，利用回调函数的写法，将获取的表单信息绑定在this实例身上。

````js
<Form
       ref={form => this.from = form}
       onValuesChange={this.changedata}
  ></Form>
````

![mark](http://qiniu.cloud-zhi.com/blog/210511/62bkB9bE51.png?imageslim)

能够得到一堆方法的对象，再通过getFieldsValue()方法，获取form表单的传值，再通过props将信息传入父组件即可。

既是更新，在此之前都是要能够获取要修改的值，这里是通过双向绑定的方法，input的值从状态中获取，状态中值的首次渲染通过componentWillMount周期里面获取来自父组件的props值，来确定要添加的值。再之后就根据componentWillReceiveProps周期来获取来自父组件的更新值。

#### 数据的添加

数据的添加实际上也是获取子组件表单中的数据，使用的方法跟上面的方法相同，不再赘述。

### 商品管理

商品管理的功能主要包括，商品的展示、商品的搜索、商品的状态管理、商品的添加以及修改。

#### 商品的展示

![mark](http://qiniu.cloud-zhi.com/blog/210511/fIl811GjIk.png?imageslim)

在现有的前后台交互中，获取后台数据用用于展示大致分为两种，分页获取和全部获取。**全部获取数据**可以将数据放在状态中，如无变化阅读只是从状态中读取数据，一次获取；但是面对庞大的数据，**分页获取**可以减轻服务器的压力，但是每次翻页都会重新请求数据。其实这些功能都是后台完成的，我们做的就是向后台提交申请时，带上展示条数和展示页码的数据即可。本例中利用的是antd的Table组件中的**页码监听**功能来实现动态的数据请求，每次的页码的改变都会重新调用请求函数，并将新的请求页码作为参数传入，从而实现能够动态展示需要展示的页码。

`````js
<Table
       pagination={{
             onChange: (pageNum) => this.getProducts(pageNum)
       }}
 />
`````

`````js
    getProducts = async (pageNum) => {
        this.pageNum = pageNum; //保存pageNum，让其他人看到
        const { searchType, searchInput } = this.state;
        this.setState({ loading: true })  //显示loading
        let result;  //定义结果变量
        if (searchInput) {  //如果有关键词，采用搜索分页
            result = await reqSearchProducts(pageNum, PAGE_SIZE, searchType, searchInput)
        } else {   //如果没有关键词，采用一般分页
            result = await reqProducts(pageNum, PAGE_SIZE)
        }
        this.setState({ loading: false })  //隐藏loading
        if (result.status === 0) {
            const { total, list } = result.data;
            this.setState({
                total,
                products: list
            })
        }
    }
`````

> 分页显示
>    接口请求函数需要的数据：pageNum，pageSize
>        异步获取第一页的数据的显示
>        调用分页接口请求函数，获取到当前页的product和总记录数total
>         更新状态：produts / total
>     翻页：
>         绑定翻页的监听，监听回调需要得到pageNum
>         异步获取指定页码的数据显示

#### 商品的搜索

商品的搜索就是按照不同条件来渲染不同的页面，当然这些关键词的提炼都是由后台完成，我们要做的就是**收集由用户输入的关键词**并向后台发送含有这些关键词的请求信息，接口请求如下：

`````js
//获取搜索商品的分页列表
export const reqSearchProducts = (pageNum , pageSize , searchType , productInput) => ajax( BASE_URL + '/manage/product/search',{
  pageNum ,
  pageSize,
  [searchType] : productInput  
})//searchType是一个变量，因为有两种可能,axios.get的对象传参
`````

这里需要注意的是，**searchType的[]写法**，通常我们在对象的属性值可以使用任意的变量或是字符创，无需特殊声明，而属性需要使用[]包裹的方式来体现出我们的属性是一个**变量**。普通的写法 key : value，或是'key' : value，都会被JavaScript解析为后者字符串的形式。

这里的搜索方式和搜索的关键词通过我们用户选择和输入来传递给后台，相关代码已经在上面显示。我们根据有没有关键词的输入来体现出需不需要搜索展示。我们通过状态来获取searchType和searchInput，根据antd不同的获取value值的方法将得到关键词放在状态中。之后通过点击事件重新获取分页搜索的第一页。

`````jsx
<Select value={searchType} style={{ width: 150 }} onChange={value => this.setState({ searchType: value })}>
                    <Option value='productName'>按名称搜索</Option>
                    <Option value='productDesc'>按描述搜索</Option>
                </Select>
                <Input placeholder='关键字' style={{ width: 150, margin: '0 15px' }} onChange={e => this.setState({ searchInput: e.target.value })} />
                <Button type='primary' onClick={() => this.getProducts(1)} >搜索</Button>
`````

> 搜索分页
>
>  接口函数所需要的数据
>
> ​    pageSize, pageNum , productType等
>
>   异步更新搜索显示分页
>
> ​    如果searchName有值，调用搜索函数的函数获取数据并更新状态

#### 商品的状态管理

商品的状态管理就是显示商品的在售和下架状态，并且可以手动的来控制这个状态。这里补充一下antd的Table组件中**columns属性**的配置。

````jsx
        const columns = [
            {
                title: '价格',
                width: 150,
                dataIndex: 'price',
                render: (price) => '￥' + price  //当前dataindex指定了对应的属性，传入对应的属性值；不指定就会是当前对象
            },
            {
                title: '状态',
                width: 150,
                // dataIndex: 'status',
                render: (product) => {
                    const { status, _id } = product
                    return (
                        <span>
                            <Button
                                type='primary'
                                onClick={() => this.updateStatus(_id, status === 1 ? 2 : 1)}
                            >
                                {status === 1 ? '下架' : '上架'}
                            </Button>
                            <span> {status === 1 ? '在售' : '已下架'} </span>
                        </span>
                    )
                }
            },
        ];
````

关于在配置中，观察上面两个示例，如果指定了数据来源（第一个对象），即**指定了dataIndex**，再对其使用render，此时的回调函数支持传入的参数就是这**数据来源**。如果没有指定数据来源，即**没有指定dateInde**，此时render的回调函数所支持的回调函数就是**当前的传入对象**，你可以获取这个来自这个对象的全部信息。其中就包括商品信息的状态值和id值，更改后向后台发送更改的请求数据。这里可以观察一下**三目运算符**的写法。

````jsx
const result = await reqUpdateStatus(_id, newStatus);
````

#### 商品的详情

商品的详情就是分类展示信息功能实现，这里补充四个知识点。

``````jsx
{
                title: '操作',
                render: (product) => {
                    return (
                        <span>
                            <button style={{ outline: 'none', border: 'none', cursor: 'pointer', background: 'transparent', color: '#1890ff' }} onClick={() => this.props.history.push('/product/detail', product)} >详情</button>  {/*push方法的第二个参数，可以将product通过location传到目标组件 */}
                            <br></br>
                            <button style={{ outline: 'none', border: 'none', cursor: 'pointer', background: 'transparent', color: '#1890ff' }} onClick={() => this.props.history.push('/product/addupdate', product)}>修改</button>
                        </span>
                    )
                }
            },
``````

- **编程式路由的push方法的第二个参数**

  `````jsx
  this.props.history.push('/product/detail', product)
  `````

  可以传递两个参数，第一个是路径，第二个则是附带向目标路由传递的信息，这里传递的是这个点击事件选中商品的render中的product。目标路由中通过location中的state接收。

  ````jsx
  this.props.location.state
  ````

- **父子组件中互相调用方法**

   1、子组件调用父组件的方法：将父组件的方法以函数属性的形式传递给子组件，子组件就可以调用

   2、父组件调用子组件的方法：在父组件中通过ref得到子组件标签对象（也就是说组件对象），调用其方法。

- 安全的插入来自服务器带有标签的数据，如：\<p>...\</p>

  ````jsx
  <span dangerouslySetInnerHTML={{ __html: detail }}></span>  {/*插入HTML代码 */}
  ````

  在react中，通过富文本编辑器进行操作后的内容，会保留原有的标签样式，并不能正确展示。用上面的代码可以正确显示。

  不合时宜的使用 innerHTML 可能会导致 cross-site scripting (XSS) 攻击。 净化用户的输入来显示的时候，经常会出现错误，不合适的净化也是导致网页攻击的原因之一。dangerouslySetInnerHTML 这个 prop 的命名是故意这么设计的，以此来警告，它的 prop 值（ 一个对象而不是字符串 ）应该被用来表明净化后的数据。

- Promise.all([promise1,promise2])的使用

#### 商品的添加

商品的添加和修改共用一个页面，区别是在于是否获取此次选中的商品的信息。商品的信息的获取也是从push方法中获得

````js
const product = this.props.location.state   //获取
````

关键代码

`````js
this.isUpdate = !!product;   //将product强行的转化为布尔值，借此来表示是否要更新或是添加
this.product = product || {};  //储存商品信息，或者{}是为了防止报错，同时如果是添加也就啥也不显示了
`````

通过由push传过来的单个商品信息和{}空集取或，意为如果product里面有值取product，若是undefined取{}空集。后经判断是添加或是修改来确定显示。

添加的时候，表单获取所有的输入值，取得关键信息提交给后台发送添加请求。当然在此之前会有一个表单验证的功能，这里借用的是Form组件自带的rules属性判断即可。

#### 商品的修改

原理上文已解释清楚，不再赘述。

## 角色管理

## 用户管理

## 图形图表的显示







