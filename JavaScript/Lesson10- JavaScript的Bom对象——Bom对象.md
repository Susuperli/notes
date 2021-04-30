# 第十讲 JavaScript的Dom和Bom对象——Bom对象

## 概述

- DOM：文档对象模型，document object model，当前载入页面的所拥有的对象，代表当前文档。
- BOM：浏览器对象模型，Browser object model，页面以外所有的对象，代表浏览器窗口和桌面屏幕。

## Bom对象

### window对象

#### 属性

- window.innerHeight：浏览器窗口的实际高度（不包括工具栏和滚动条）。
- window.innerWidth：浏览器窗口的实际宽度（不包括工具栏和滚动条）。
- length：设置或返回窗口中的框架数量。

#### 方法

- alert()：带有确认信息的提示框。

- confirm()：带有确认和取消的提示框。

- prompt()：带有输入信息的提示框。

- window.open("URL","窗口名称(一般是不好使，但是不设置第二个就不能设置第三个了)","属性=值,属性=值,属性=值")：打开一个新的网页。

- window.print()：打印当前页面内容。

- window.close()：关闭当前浏览器页面。

- window.resizeBy()：调整窗口的宽度和高度（仅IE支持，了解即可）。

- window.resizeTo()：调整窗口到宽度和高度（仅IE支持，了解即可）。

- window.scrollBy(x,y)：按照指定像素值来滚动内容。

- window.scrollTo(x,y)：把内容滚动到指的坐标。

- setTimeout()：在指定的毫秒数后调用函数或计算表达式。

  ````js
  setTimeout(function(){
  	   document.getElementById("con").style.width="300px";
     },2000);
  ````

- clearTimeout()：取消由setTimeout()方法设置的timeout。

  ````js
   i=setTimeout(function(){
  	   document.getElementById("con").style.width="300px";
     },2000);
     function stopchange(){
  	   clearTimeout(i);
     }
  ````

- setInterval()：在指定的周期（以毫秒计时）来定时。

- clearInterval()：取消由setInterval()设置的interval。

### navigator 对象

#### 方法

- appCodeName：返回浏览器的代码。
- **appVersion：返回平台和版本信息。**
- APPName：返回浏览器名称。
- browserLanguage：返回浏览器语言。
- **cookieEnabled：返回指明浏览器中是否启用cookie的布尔值。**
- platform：返回完整操纵系统。
- userAgent：返回又客户完成机发送服务器的uer-agent头部信息。

### screen对象

包含有关客户端显示屏的信息。

#### 属性

- screen.availHeight：返回屏幕的高度（除去widows任务栏）。

- screen.availWidth：返回屏幕的宽度（除去windows任务栏）。

- screen.height：返回屏幕的高度。

- screen.width：返回屏幕的宽度。

- 注意区分和和inner.Height的区别

  ````js
  <script type="text/javascript">
  	iw=window.innerWidth;
  	ih=window.innerHeight;
  
  	ah=screen.availHeight;
  	aw=screen.availWidth;
  	
  	h=screen.height;
  	w=screen.width;
  	
  	document.write("<div>"+iw+","+ih+"</div>")
  	document.write("<div>"+aw+","+ah+"</div>")
  	document.write("<div>"+w+","+h+"</div>")
  </script>
  ````

  ![image-20201220114632095](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201220114632095.png)

### history对象

包含用户（在浏览器中）访问过的URL。History 对象是 **window 对象的一部分**，可通过 window.history 属性对其进行访问

#### 属性

length：返回历史列表中的网址数。

#### 方法

- history.back()：加载返回浏览器历史列表中前一个URL。
- history.forward()：加载返回浏览器历史记录的下一个URL。
- history.go()：加载 history 列表中的某个具体页面。

### Location对象

Location 对象包含有关当前 URL 的信息。

Location 对象是 **window 对象的一部分**，可通过 window.Location 属性对其进行访问。

**注意：** 没有应用于Location对象的公开标准，不过所有浏览器都支持该对象。

#### 方法

- location.hash： 设置或返回从井号 (#) 开始的 URL（锚）。

- location.host：设置或返回主机名和当前 URL 的端口号。

- location.hostname：设置或返回当前 URL 的主机名。

- **location.href：设置或返回完整的URL地址。**

  ````js
  <script type="text/javascript">
      document.write(location.href);
  </script>
  ````

  ![image-20201220150418417](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201220150418417.png)

  这里面得到的是当前文档的完整的路径，其中中文部分浏览器自动转码。

- location.pathname：设置或返回当前 URL 的路径部分。

- location.protocol： 设置或返回当前 URL 的协议。

- **location.search： 设置或返回从问号 (?) 开始的 URL（查询部分）。**

  location.search1：

  ````js
  	<div>
  		欢迎您来到我的主页
  	</div>
  	<a href="js10 location-search2.html?name=lily&sex=lady&age=18" target="_blank">点我一下</a>
  ````

  location.search2：

  ````js
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>location.search2</title>
  </head>
  <style>
      ul{
          list-style: none;
      }
  </style>
  <body>
      <ul id="list">
  
      </ul>
  </body>
  <script>
      var queryString=location.search;//?name=lily&sex=lady&age=18
      var qs=queryString.slice(1);//name=lily&sex=lady&age=18
      var qa=qs.split("&");//name=lily,sex=lady,age=18
      var qname=[];
      var qvalue=[];
      for(var i in qa){
          var qaa=qa[i].split("=");
          qname.push(qaa[0]);
          qvalue.push(qaa[1]);
      }
      for(var j in qname){
          document.getElementById("list").innerHTML+="<li>"+qname[j]+":"+qvalue[j]+"</li>";
      }
  </script>
  </html>
  ````

  ![image-20201220162345065](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201220162345065.png)

## 补充内容

### 滚动效果

````js
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
	<style type="text/css">
		div{
			height: 11120px;
		}
	</style>
</head>
<body>
	<div>
		
	</div>
</body>
<script type="text/javascript">
	window.onscroll=function(){
		var s=document.documentElement.scrollTop;
		console.log(s);
	}
</script>
</html>
````

![image-20201220164354946](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201220164354946.png)

![Windowsobject](D:\0-Link\naotes\picture\Windowsobject.gif)