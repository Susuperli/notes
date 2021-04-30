# 第六讲 本地存储和离线存储

## 本地存储

### cookie

cookie的设计的初衷是给服务器端脚本用来存储少量的数据，该数据每次请求一个相关的url时传递到服务器中，不同浏览器对于本地cookie的数量都有一定的限制，不允许大量的使用cookie，且不大于4kb。

#### 概述

cookie是网站向客户端文件夹中的变量值相关信息，方便网站实现一些特殊的功能。（例如购物车功能）。

#### 大小限制

- IE:50
- FF:50
- Opera:30
- Safari/Webkit理论上没有个数限制，但是很多也会导致错误

#### 判断是否支持cookie

````js
if(navigator.cookieEnable) //判断是否支持
````

#### 创建

创建并设置cookie过期时间

`````js
document.cookie="userName=123&pwd=abc;expires=时间"
`````

````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>cookie</title>
</head>

<body>
    用户名：<input type="text" name="username" id="username"><br>
    密码：<input type="password" id="pwd"><br>
    <button id="btn">登录</button>
</body>
<script>
    if (document.cookie) {
        var coo = document.cookie;
        var un = coo.split("=")[1];
        document.getElementById("username").value = un;
    }
    document.getElementById("btn").onclick = function () {
        var username = document.getElementById("username").value;
        var pwd = document.getElementById("pwd").value;
        var xml = new XMLHttpRequest();
        xml.open("post", "http://www.qhdlink-student.top/student/login.php");
        xml.setRequestHeader("content-type", "application/x-www-form-urlencoded");
        xml.send("username=" + username + "&userpwd=" + pwd + "&userclass=64&type=4");
        xml.onreadystatechange = function () {
            if (this.readyState == 4 && this.status == 200) {
                var data = this.responseText;
                if (data == "ok") {
                    var dat = new Date();
                    document.cookie = "username=" + username + ";expires=" + dat.getTime() + 3 * 24 * 60 * 60 * 1000;
                }
            }
        }
    }
</script>
</html>
````

### web储存

web最初作为HTML5的一部分被定义成api的形式，但是后来被剥离出来作为独立的标准，目前该标准还在制定当中，但是其中一部分内容已经被所有的主流浏览器兼容。包含localStorage和sessionStorage对象

#### localStorage

- 存值

  ````js
  localStorage.属性值=值;   //直接添加
  localStorage.setItem('属性值','值');  //方法添加
  ````

- 读取

  ````js
  localStorage.属性名;
  localStorage.getItem('属性名');
  ````

- 修改

  ````js
  与存储值一样，重新赋值
  ````

- 删除

  ````js
  remove('属性名')   //删除指定项
  clear();  //全部删除
  ````

##### **注意事项**

浏览器的大小不统一，并且在IE8以上的IE版本才支持localStorage这个属性
**目前所有的浏览器中都会把localStorage的值类型限定`为string类型`，这个在对我们日常比较常见的JSON对象类型需要一些转换**
localStorage在浏览器的隐私模式下面是不可读取的
localStorage本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，会导致页面变卡
localStorage不能被爬虫抓取到

**需要转换，默认只能存储字符串模式**

`````js
var storage=window.localStorage;
var data={
     name:'zhangSan',
     sex:'1'
 };
 //将对象转换为 String ,如果不转，在存入localStorage后，读取出来转换 json对象会报错
 var setData=JSON.stringify(data); 
 storage.setItem("data",setData);
 
 //将JSON字符串转换成为JSON对象输出
 var jsonString=storage.getItem("data");
 console.log(typeof jsonString); //打印出 String;
 var jsonObj=JSON.parse(jsonString);
 console.log(typeof jsonObj); //打印出 Object;
`````

#### sessionStorage

- 用法和localStorage对象的使用方法完全一样。区别在于存储的有效时间和作用域。
- 区别
  - localStorage存储的数据是永久的，除非刻意删除。而sessionStorage的数据是临时的，当该脚本所在的最顶层的窗口或浏览器关闭之后，数据就会被删除。
  - localStorage的作用域是限定在文档源级别的（文档源是通过协议，主机名一级端口三者来确定的）同一个文档源之间的不同页面可以共享localStorage数据，可以相互读取，设置覆盖。而在sessionStorage的作用域除了被限制在文档源中，还被限制在窗口中，如果同源文档渲染在不同的浏览器标签中，他们各自的sessionStorage数据无法共享，一个标签页面中的脚本是无法读取或者覆盖有另一个标签页脚本写入的数据，哪怕这两个标签页渲染的是同一个页面，运行的是同一个脚本也不行。

## 离线储存

### 传统浏览器

传统浏览器缓存，通过浏览器来判定需要缓存网页的那些内容到本地，当再次访问该页面时，浏览器会优先从浏览器缓存中读取缓存的内容，没有被缓存的内容才会向服务器请求相关内容。只会有当缓存中读取缓存的内容，没有被缓存的内容才会向服务器请求相关内容。只有缓存过期或者用户强制缓存时才会重新向服务器请求内容。

### H5离线缓存

#### 特点

- 离线浏览：用户可以在离线状态下浏览网站内容。
- 更快的速度：因为数据被存储在本地，所以速度会更快。
- 减轻服务器的负载：浏览器只会下载在服务器上发生改变的资源。

#### 缓存

需要研发人员自己定义要缓存的页面内容，需要一个缓存的文件清单，这个文件是一个manifest后缀名的文件，使用H5就必须有这个文件。

参数如下：

- CACHE：指定你要浏览器进行离线存储的文件列表，一个文件一行。
- NETWORK：跟CACHE相反，指定浏览器一定要通过网络访问的文件列表。
- FALLBACK：如果通过网络访问失败了，就会访问紧跟着的那个在本地缓存好的文件。

#### 更新策略

HTML5的缓存更新策略是由manifest清单是否为最新版本来决定的，所以浏览器首先会根据HTTP的缓存策略去探测manifest清单是否最新，如果最新（浏览器返回304)，则不会去下载清单里指定的缓存文件来更新离线存储，如果不是最新的(浏览器返回200)，则会根据最新的manifest清单去重新下载指定的一系列文件，然后更新离线存储。这里要注意，由于判断manifest清单是否最新是利用了HTTP的缓存策略的，所以可能出现你更改了manifest文件，但是离线存储却没有更新的情况，这可能是因为你的服务器为你的manifest清单文件设置了相应的缓存头，manifest清单文件还未过期，这是浏览器并没有真正向服务器发起请求确认manifest的新鲜度，而是直接使用了缓存的manifest文件，另外一个需要注意的是，修改了一些文件以后想要让离线存储更新，就必须改动manifest清单文件。

## HTTP缓存机制

- web缓存时一种保存为资源副本并在下次请求时直接使用该副本的技术。

- web缓存可以分为这几种：浏览器缓存、CDN缓存、服务器缓存、数据库缓存。因为可能会直接使用副本免于重新发送请求或者仅仅确认资源没变无需重新传输资源实体，web缓存可以减少延迟加快网页打开速度、重复利用资源减少网络带宽消耗、降低请求次数或者减少传输内容从而减轻服务器压力。

- 浏览器HTTP缓存机制。浏览器HTTP缓存可以分为强缓存和协商缓存。强缓存和协商缓存的最大也是最根本的区别是：**强缓存**命中的话不会发送请求到服务器（比如Chrome中的200 from memory cache）；**协商缓存**一定会发送请求到服务器，通过资源的请求手字段验资源是否命中协商缓存，如果命中协商缓存，服务器会将这个请求返回，但是不会返回这个资源的实体，而是同之客户端可以从缓存中加载这个资源（304 not modified）

  ![强缓存和协商缓存](D:\0-Link\naotes\JavaScript-senior\picture\强缓存和协商缓存.jpg)

### 强缓存

### 协商缓存



