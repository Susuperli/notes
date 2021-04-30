# 第一讲 ajax

## 概述

### 概念

Ajax（Asynchronous JavaScript And XML）翻译成中文就是“异步JavaScript和XML”。即使用JavaScript语言与服务器进行异步交互，传输的数据为XML（当然，传输的数据不只是XML）。

Ajax还有一个最大的特点就是，当服务器响应时，不用刷新整个浏览器页面，而是可以局部刷新。这一特点给用户的感受是在不知不觉中完成请求和响应过程。

- 与服务器异步交互
- 浏览器页面局部刷新

### 同步和异步区别

- 同步交互：客户端发出一个请求后，需要等待服务器响应结束后，才能发出第二个请求。
- 异步交互：客户端发出一个请求后，无需等待服务器响应结束，就可以发出第二个请求。![同步异步区别](D:\0-Link\naotes\JavaScript-senior\picture\同步异步区别.png)

### Ajax所包含的技术

大家都知道ajax并非一种新的技术，而是几种原有技术的结合体。它由下列技术组合而成。

> 1.使用CSS和XHTML来表示。
>
> 2.使用DOM模型来交互和动态显示。
>
> 3.使用XMLHttpRequest来和服务器进行异步通信。
>
> 4.使用javascript来绑定和调用。

### Ajax工作原理

![ajax工作原理](D:\0-Link\naotes\JavaScript-senior\picture\ajax工作原理.png)

![普通交互](D:\0-Link\naotes\JavaScript-senior\picture\普通交互.jpg)

![ajax交互](D:\0-Link\naotes\JavaScript-senior\picture\ajax交互.jpg)

## Ajax应用

### 创建

````js
var xhr=new XMLHttpRequest() //标准创建方式
		
var xmlHttp//兼容方法
		if(window.XMLHttpRequest){
			xmlHttp=new XMLHttpRequest();
		}else{
			xmlHttp=new ActiveXObject("Microsoft.XMLHTTP")//IE6情况
		}
````

### 属性

- **readyState**

  存储状态码，readyState 属性存有 XMLHttpRequest 的状态信息。

  **0**：（未初始化）xhr对象已经创建，但还没有调用open()方法。值为0表示对象已经存在，否则浏览器会报错：对象不存在。
  **1** :（载入/发送请求）调用open()方法对xhr对象进行初始化，根据参数(method,url,true)，完成对象状态的设置。并调用send()方法开始向服务端发送请求。值为1表示正在向服务端发送请求。
  **2** ：（载入完成/响应接收）接收服务器端响应回的数据。但获得的还只是服务端响应的原始数据，并不能直接在客户端使用。值为2表示send()请求方法执行完成，并已经接收完全部的响应数据（未解析）。
  **3** － （交互/解析数据）正在解析从服务器端接收到的响应数据。即根据服务器端响应头部返回的MIME类型把数据转换成能通过responseBody、responseText或responseXML属性存取的格式，为在客户端调用作好准备。值为3表示正在解析数据。
  **4** － （后台处理完成）响应内容解析完成，可以在客户端调用了。此阶段确认全部数据都已经解析为客户端可用的格式，解析已经完成。值为4表示数据解析完毕，可以通过XMLHttpRequest对象的相应属性取得数据。

  总之，整个XMLHttpRequest对象的生命周期应该包含如下阶段：
  创建－0初始化请求－1发送请求－2接收数据－3解析数据－4完成 

- **status**

  1** ：请求收到，继续处理
  2** ：操作成功收到，分析、接受
  3** ：完成此请求必须进一步处理
  4** ：请求包含一个错误语法或不能完成
  5** ：服务器执行一个完全有效请求失败
  100——客户必须继续发出请求
  101——客户要求服务器根据请求转换HTTP协议版本
  **200——交易成功**
  201——提示知道新文件的URL
  202——接受和处理、但处理未完成
  203——返回信息不确定或不完整
  204——请求收到，但返回信息为空
  205——服务器完成了请求，用户代理必须复位当前已经浏览过的文件
  206——服务器已经完成了部分用户的GET请求
  300——请求的资源可在多处得到
  301——删除请求数据
  302——在其他地址发现了请求数据
  303——建议客户访问其他URL或访问方式
  304——客户端已经执行了GET，但文件未变化
  305——请求的资源必须从服务器指定的地址得到
  306——前一版本HTTP中使用的代码，现行版本中不再使用
  307——申明请求的资源临时性删除
  400——错误请求，如语法错误
  401——请求授权失败
  402——保留有效ChargeTo头响应
  403——请求不允许
  **404——没有发现文件、查询或URl**
  405——用户在Request-Line字段定义的方法不允许
  406——根据用户发送的Accept拖，请求资源不可访问
  407——类似401，用户必须首先在代理服务器上得到授权
  408——客户端没有在用户指定的饿时间内完成请求
  409——对当前资源状态，请求不能完成
  410——服务器上不再有此资源且无进一步的参考地址
  411——服务器拒绝用户定义的Content-Length属性请求
  412——一个或多个请求头字段在当前请求中错误
  413——请求的资源大于服务器允许的大小
  414——请求的资源URL长于服务器允许的长度
  415——请求资源不支持请求项目格式
  416——请求中包含Range请求头字段，在当前请求资源范围内没有range指示值，请求也不包含If-Range请求头字段
  417——服务器不满足请求Expect头字段指定的期望值，如果是代理服务器，可能是下一级服务器不能满足请求
  **500——服务器产生内部错误**
  501——服务器不支持请求的函数
  502——服务器暂时不可用，有时是为了防止发生系统过载
  **503——服务器过载或暂停维修**
  504——关口过载，服务器使用另一个关口或服务来响应用户，等待时间设定值较长
  505——服务器不支持或拒绝支请求头中指定的HTTP版本

- **responseText**

  **获得字符串形式的来自服务器的响应数据**

- responseXML

  获得 XML 形式的响应数据，用得少。

### 事件

- onreadystatechange

  当请求被发送到服务器时，我们需要执行一些基于响应的任务。每当 readyState 改变时，就会触发 onreadystatechange 事件。

### 方法

| 方法                         | 描述                                                         |
| :--------------------------- | :----------------------------------------------------------- |
| open(*method*,*url*,*async*) | 规定请求的类型、URL 以及是否异步处理请求。                                                                                                                                         *method*：请求的类型；GET 或 POST                                                                                                                                                              *url*：文件在服务器上的位置                                                                                                                                                                       *async*：true（异步）或 false（同步） |
| send(*string*)               | 将请求发送到服务器。*string*                                 |
| setRequestHeader()           | 设置请求头                                                   |

![设置请求头](D:\0-Link\naotes\JavaScript-senior\picture\设置请求头.png)

````html
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
</head>
<body>
	<div class="">
		用户名：<input type="text" id="username" name="username"/>
		密码：<input type="password" id="password" name="uerpwd"/>
		班级：<input type="text" id="class" name="userclass"/>
		权限号码：<input type="text" id="number" name="usertype"/>
		<button type="button" id="btn">登录</button>
	</div>
</body>
<script type="text/javascript">
	function login(){
		//第一步创建
		var xhr;
		if(window.XMLHttpRequest){
			xhr=new XMLHttpRequest()
		}else{
			xhr=new ActiveXObject("Microsoft.XMLHTTP")
		}
		//第二步，初始化ajax对象
		xhr.open("post","http://www.qhdlink-student.top/student/login.php")
		//第三步，设置发送信息的头部信息(数据类型)
		xhr.setRequestHeader("content-type","application/x-www-form-urlencoded")
		// 第四步,拼接及发送数据
		var uname=document.getElementById("username").value;
		var upass=document.getElementById("password").value;
		var uclas=document.getElementById("class").value;
		var unumb=document.getElementById("number").value;
		var date="username="+uname+"&userpwd="+upass+"&userclass="+uclas+"&type="+unumb;   //拼接数据
		xhr.send(date)   //发送数据
		console.log(date)
		// 第五步,判断状态,接受并处理数据
		xhr.onreadystatechange=function(){//状态码发生变化时触发
			if(xhr.readyState==4 && xhr.status==200){
				var reDate=xhr.responseText;  //获取服务器响应的数据
				if(reDate=="ok"){
					alert("登陆成功")
				}else{
					alert("登陆失败")
				}
			}
		}
	}
	document.getElementById("btn").onclick=login
</script>
</html>
````

## jQuery中Ajax对象

### 创建

`````js
$(function(){
    $.ajax({
            url:"http://www.qhdlink-student.top/student/login.php",   //地址 
            dataType: "text ",    //服务器数据返回类型
            type: "get",  //传输方式
            data: {
                "username":"zyp",
                "userpwd": "123456",
                "userclass": "64",
                "type": "4",
                "async": "true",
            }, 
            success:function(data){    //传输成功
                console.log(data)
            },
            error:function(){       //传输出错
                console.log(error)
            }
    })
})
`````

#### 参数说明

- url：地址。
- dataType：预期服务器返回的数据类型，包括：xml、html、json、text等，可以省略。
- type：get/post。
- data：发送给服务器的数据，这里使用json对象。
- async：设置交互异步还是同步，默认是true。
- success：请求成功回调函数，给函数设置形参来接受返回json数据。

### 其他方法

````js
$.get(url,callback)      $.post(url,data,callback)
````

`````js
 $.post("http://www.qhdlink-student.top/student/login.php",{"username":"zyp","userpwd": "123456","userclass": "64","type": "4","async": "true"},function(data){
            console.log(data)
        })
`````

## HTML5 WebSocket

### 简介

WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。

WebSocket 使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在 WebSocket API 中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。

在 WebSocket API 中，浏览器和服务器只需要做一个握手的动作，然后，浏览器和服务器之间就形成了一条快速通道。两者之间就直接可以数据互相传送。

现在，很多网站为了实现推送技术，所用的技术都是 Ajax 轮询。轮询是在特定的的时间间隔（如每1秒），由浏览器对服务器发出HTTP请求，然后由服务器返回最新的数据给客户端的浏览器。这种传统的模式带来很明显的缺点，即浏览器需要不断的向服务器发出请求，然而HTTP请求可能包含较长的头部，其中真正有效的数据可能只是很小的一部分，显然这样会浪费很多的带宽等资源。

HTML5 定义的 WebSocket 协议，能更好的节省服务器资源和带宽，并且能够更实时地进行通讯。

![ws](D:\0-Link\naotes\JavaScript-senior\picture\ws.png)

### 使用场景

- 社交订阅
- 多玩家游戏
- 协同编写
- 股票经济
- 体育实况跟新
- 多媒体聊天
- 基于位置的应用
- 在线教育

### 原理

浏览器通过 JavaScript 向服务器发出建立 WebSocket 连接的请求，连接建立以后，客户端和服务器端就可以通过 TCP 连接直接交换数据。

当你获取 Web Socket 连接后，你可以通过 **send()** 方法来向服务器发送数据，并通过 **onmessage** 事件来接收服务器返回的数据。

WebSocket看成是一种类似TCP/IP的socket技术；此socket在Web应用中实现，并获得了和TCP/IP通信一样灵活方便的全双向通信功能。

WebSocket协议由RFC 6455定义。协议分为两个部分： 握手阶段和数据通信阶段。

WebSocket为应用层协议，其定义在TCP/IP协议栈之上。WebSocket连接服务器的URI以"ws"或者"wss"开头。ws开头的默认TCP端口为80，wss开头的默认端口为443。

原文链接：https://blog.csdn.net/yinqingwang/article/details/52565133

以下 API 用于创建 WebSocket 对象。

`````js
var Socket = new WebSocket(url, [protocol] );
`````

````html
<!DOCTYPE HTML>
<html>
   <head>
   <meta charset="utf-8">
   <title>菜鸟教程(runoob.com)</title>
    
      <script type="text/javascript">
         function WebSocketTest()
         {
            if ("WebSocket" in window)
            {
               alert("您的浏览器支持 WebSocket!");
               
               // 打开一个 web socket
               var ws = new WebSocket("ws://localhost:9998/echo");
                
               ws.onopen = function()
               {
                  // Web Socket 已连接上，使用 send() 方法发送数据
                  ws.send("发送数据");
                  alert("数据发送中...");
               };
                
               ws.onmessage = function (evt) 
               { 
                  var received_msg = evt.data;
                  alert("数据已接收...");
               };
                
               ws.onclose = function()
               { 
                  // 关闭 websocket
                  alert("连接已关闭..."); 
               };
            }
            
            else
            {
               // 浏览器不支持 WebSocket
               alert("您的浏览器不支持 WebSocket!");
            }
         }
      </script>
        
   </head>
   <body>
   
      <div id="sse">
         <a href="javascript:WebSocketTest()">运行 WebSocket</a>
      </div>
      
   </body>
</html>
````

## Ajax数据处理

### Json简介

JSON是JavaScript Object Notation的简称，中文含义为“JavaScript 对象表示法”，**它是一种基于文本，独立于语言的轻量级数据交换格式，**而不是一种编程语言。

JSON 是一种轻量级的数据交换格式，它基于 ECMAScript (w3c制定的js规范)的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。

### Json特点

- JSON 是纯文本
- JSON 具有“自我描述性”（人类可读）
- JSON 具有层级结构（值中存在值）
- JSON 可通过 JavaScript 进行解析
- JSON 数据可使用 AJAX 进行传输

### 语法规则

```js
var json = {
        键 : 值,
        键 : 值,
        .....
    }
```

 说明 ： json中的键 用双引号括起来 值可以是任意类型的数据 （ 严格的json值不会出现function (){...}  严格的json键用双引号括起来）

![json语法规则](D:\0-Link\naotes\JavaScript-senior\picture\json语法规则.png)



### Json对象和字符串之间的转换

客户端提交过来的数据一般都是json字符串，有了更好地进行操作（面向对象的方式），所以我们一般都会想办法将json字符串转换为json对象。

JSON.parse( )  将字符串转为对象

JSON.stringify( ) 将对象（{ } [ ]）转为字符串

## FormData对象

### 简介

![formdata对象](D:\0-Link\naotes\JavaScript-senior\picture\formdata对象.png)

### 构造函数

创建一个formData对象实例有几种方式

1、创建一个`空对象`实例

```js
var formData = new FormData();
```

此时可以调用append()方法来添加数据

2、使用已有的表单来初始化一个对象实例

假如现在页面已经有一个表单

```js
<form id="myForm" action="" method="post">
    <input type="text" name="name">名字
    <input type="password" name="psw">密码
    <input type="submit" value="提交">
</form>
```

我们可以使用这个表单元素作为初始化参数，来实例化一个formData对象](javascript:void(0);)

```js
// 获取页面已有的一个form表单
var form = document.getElementById("myForm");
// 用表单来初始化
var formData = new FormData(form);
// 我们可以根据name来访问表单中的字段
var name = formData.get("name"); // 获取名字
var psw = formData.get("psw"); // 获取密码
// 当然也可以在此基础上，添加其他数据
formData.append("token","kshdfiwi3rh");
```

###  操作方法

首先，我们要明确formData里面存储的数据形式，一对key/value组成一条数据，key是唯一的，一个key可能对应多个value。如果是使用表单初始化，每一个表单字段对应一条数据，它们的HTML name属性即为key值，它们value属性对应value值。

| key  | value      |
| ---- | ---------- |
| k1   | [v1,v2,v3] |
| k2   | v4         |

#### 获取值

我们可以通过get(key)/getAll(key)来获取对应的value

```js
formData.get("name"); // 获取key为name的第一个值
formData.get("name"); // 返回一个数组，获取key为name的所有值
```

#### 添加数据

我们可以通过append(key, value)来添加数据，如果指定的key不存在则会新增一条数据，如果key存在，则添加到数据的末尾

```js
formData.append("k1", "v1");
formData.append("k1", "v2");
formData.append("k1", "v1");
 
formData.get("k1"); // "v1"
formData.getAll("k1"); // ["v1","v2","v1"]
```

#### 设置修改数据

我们可以通过set(key, value)来设置修改数据，如果指定的key不存在则会新增一条，如果存在，则会修改对应的value值。

```js
formData.append("k1", "v1");
formData.set("k1", "1");
formData.getAll("k1"); // ["1"]
```

 #### 判断是否该数

我们可以通过has(key)来判断是否对应的key值

```js
formData.append("k1", "v1");
formData.append("k2",null);
 
formData.has("k1"); // true
formData.has("k2"); // true
formData.has("k3"); // false
```

####  删除数据

通过delete(key)，来删除数据

```js
formData.append("k1", "v1");
formData.append("k1", "v2");
formData.append("k1", "v1");
formData.delete("k1");
 
formData.getAll("k1"); // []
```

####  遍历

我们可以通过entries()来获取一个迭代器，然后遍历所有的数据

```js
formData.append("k1", "v1");
formData.append("k1", "v2");
formData.append("k2", "v1");
 
var i = formData.entries();
 
i.next(); // {done:false, value:["k1", "v1"]}
i.next(); // {done:fase, value:["k1", "v2"]}
i.next(); // {done:fase, value:["k2", "v1"]}
i.next(); // {done:true, value:undefined}
```

可以看到返回迭代器的规则

1. 每调用一次next()返回一条数据，数据的顺序由添加的顺序决定
2. 返回的是一个对象，当其done属性为true时，说明已经遍历完所有的数据，这个也可以作为判断的依据
3. 返回的对象的value属性以数组形式存储了一对key/value，数组下标0为key，下标1为value，如果一个key值对应多个value，会变成多对key/value返回

#### 发送数据

我们可以通过xhr来发送数据

```js
var xhr = new XMLHttpRequest();
xhr.open("post","login");
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
xhr.send(formData);
```

这种方式可以来实现文件的异步上传





