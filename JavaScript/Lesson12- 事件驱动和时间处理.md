#    第十二讲 事件驱动和时间处理

## 事件驱动概述

事件：窗体、对象、鼠标、键盘动作成为事件。

事件驱动的过程：

- 首先，在这个对象上**绑定**这个事件。
- 其次，又对这个对象上发生了这个事件。
- 最后，系统（js解释器）自动调用处理函数进行响应。

## 事件的绑定方式

- 行内绑定（不建议）：无法实现标记和动作分离

- 对象名.事件名=function(){语句;语句;}

  ````html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <style>
      div{
          width: 200px;
          height: 200px;
          border: black solid 1px;
      }
  </style>
  <body>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
  </body>
  <script>
      // document.getElementById("con").onclick=function(){
      //     this.style.background="red"  //触发当前函数的对象
      // }
      var divlist=document.getElementsByTagName("div");
      for(var i=0;i<divlist.length;i++){
          divlist[i].onclick=function(){
              this.style.background="red";
          }
      }
  </script>
  </html>
  ````

- 对象名.addEventListener("事件名",函数名,捕获过程true/冒泡过程false(默认是))。**事件名不带on**。

  说明：IE6/7/8的兼容方式是：对象名.attachEvent("on事件名",函数)。

  ````js
  if(window.addEventListener){1
      对象名.addEventListener();
  }else{
      对象名.attachEvent();   
  }
  ````

  ````html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <style>
      div{
          width: 100px;
          height: 100px;
          border: solid black 1px;
      }
  </style>
  <body>
      <div id="con"></div>
  </body>
  <script>
      var divlist=document.getElementById("con");
      divlist.addEventListener("click",function(){
          this.style.background="green";
      },false)
  </script>
  </html>
  ````


## 事件类型

### HTML相关事件（窗体和文档相关事件）

- onload事件

  包含的内容将在文档完全加载完成后触发。**window.onload事件只可以用一次，多次用会覆盖**。

  ````html
  <script>
          window.onload=function(){                  //window.onload事件只可以用一次，多次用会覆盖
              document.getElementById("con").innerHTML="hello world"
          }
      </script> 
  ````

  onunload：卸载文件。

  支持该事件的标记：\<body>、\<frame>、\<frameset>、\<iframe>、\<img>、\<link>、\<script>

- onresize事件

  当调整窗口大小的时候就会触发，在pc端的兼容性不是很好，多用于移动端的开发。

  ````js
   window.onresize=function(){
          var w=this.innerWidth;
          var h=this.innerHeight;
          document.getElementById("con").innerHTML=w+","+h;
      }
  ````

  媒介查询

  ````js
  function changefs(){
          var w=this.innerWidth;     //this指向window
          var fs=w*100/640;
          document.getElementsByTagName("html")[0].style.fontSize=fs+"px";
      }
      window.onresize=changefs;
      changefs();
  ````

- onscroll事件

  滚动事件，滚动条发生变化时触发的事件

  ````html
  <script>
      window.onscroll=function(){
          var st=document.documentElement.scrollTop;  //获取滚动条的位置
          if(st>=200){
              document.getElementById("nav").className="fix";
          }else{
              document.getElementById("nav").className="";
          }
      }
  </script>
  ````

### 键盘鼠标相关事件

- onclick单击事件

- ondblclick双击事件

- onmousedown左键按下

- onmouseup左键抬起

- onmouseover获取鼠标

  此外还有onmouseenter

- onmouseout失去鼠标

  onmouseleave  

  ````html
  <script>
      document.getElementById("footer").onmouseover=function(){
          document.getElementById("footer").style.display="none"
      }
      document.getElementById("footer").onmouseout=function(){
          document.getElementById("footer").style.display="block"
      }
  </script>
  ````

  onmousemove跟随鼠标
  
  ````js
  <script>
      document.getElementById("foot").onmousemove=function(){  //鼠标移动事件，鼠标移动就会触发。
          this.innerHTML+="move ";
      }
  ````
  
- onkeydown键盘按下

  键盘按下时触发事件

- onkeyup键盘抬起

  ````html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <body>
      <textarea name="aaa" id="con" cols="30" rows="10"></textarea>
  
      <p><span id="num">0</span>/15</p>
  </body>
  <script>
      document.getElementById("con").onkeyup=function(){  //键盘抬起出发。
         
          var len=this.value.length;  //获取文本框中的字符长度 
          document.getElementById("num").innerHTML=len;   //长度写到文档里面
          if(len>=15 ){    //判定条件
              var str=this.value.slice(0,15);  //值截取前15个字符，赋值给字符串
              this.value=str;    //字符串赋值给input的value
              document.getElementById("num").innerHTML=str.length;  //字符显示不能超过字符串的长度
          }
      }
  </script>
  </html>
  ````

  限制输入的字符串长度

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/1If8I06A54.png?imageslim)

- onkeypress按键盘

### 表单相关事件

- onchange改变事件

  按键抬起时执行

- oninput改变事件

  写入立刻执行

  ````js
      document.getElementById("username").onchange=function(){         //获取内容并且绑定事件
  
          var len=this.value.length;
          
          if(len<3){
              var ssss=this.nextSibling.innerHTML="长度不能小于三个字符";  //不可以有空格
              console.log(ssss);
          }else{
              this.nextSibling.innerHTML="用户名可用";
          }
      }
      document.getElementById("myform").onsubmit=function(){
          var s=this.children[1].innerHTML;
          if(s==="长度不能小于三个字符"||s==="*"){
              return false;
          }
      }
  ````

- onfocus获得焦点

- onblur失去焦点

  ````js
   //焦点事件
      document.getElementById("username").onfocus=function(){
          var con=this.value
          if(con=="请输入用户名")
          this.value="";
      }
      document.getElementById("username").onblur=function(){
          // var con=this.value;
          var con=this.value.trim()  //去除字符串前后空格
          if(con=="")
          this.value="请输入用户名";
      }
  ````

- onreset重置（绑到表单上）

  ````js
  //表单重置
      document.getElementById("myform").onreset=function(){
          var x=window.confirm("您确定要重置");
          if(!x){
              return false;   //阻止表单重置
          }
      }
  ````

- onsubmit提交（绑到表单上）















