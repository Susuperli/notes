# 第十三讲 事件对象

## 概念

**事件对象是用来记录一些事件发生时的相关信息的对象，事件对象是作为参数传递给处理函数的（IE8及其之前的版本并不支持）**

事件对象的创建

- Chrome支持e和window.event；

- firefox仅支持e；

- IE9支持e和window.event；

- IE8以下仅支持window.event；

- 兼容性写法

  e=window.event||e

  ````js
  document.getElementById("con").onmousemove=function(e){
          e=window.event||e;  //获取对象的兼容性高写法
          console.log(e);
          e.target.innerHTML=e.clientX+","+e.clientY;
  }
  ````

## 属性

- shiftkey：键盘shift，如果按下则返回为true。

- ctrlkey：键盘ctrl，如果按下则返回为true。

- altkey：键盘alt，如果按下则返回为true。

- **target：返回触发当前事件的对象（很大程度和this相同，稍有区别）**

  说明：IE6/7/8兼容性写法srcElement。

  **target 事件属性可返回事件的目标节点（触发该事件的节点），如生成事件的元素、文档或窗口。**

- **type**：返回当前事件的名称。

- **screenX**：鼠标指针的屏幕的水平坐标。

- **screenY**：鼠标指针的屏幕的垂直坐标。

- **clientX**：鼠标指针相对于窗口的水平坐标，不包括左右侧边栏和滚动条。

- **clientY**：鼠标指针相对于窗口的垂直坐标，不包括左右侧边栏和滚动条。

  IE6/7/8写法 x  y。

  Firefox写法：pageX pageY，也支持clientX clientY

  ```js
   document.getElementById("con").onmousemove=function(e){  //设置形参e，绑定鼠标事件，鼠标每次移动都会触发。
          e=window.event||e;  //获取对象的兼容性高写法
          e.target.innerHTML=e.clientX+","+e.clientY;
   }
  ```

- **offsetX：**相对于对象区域的X坐标。

- **offsetY**：相对于对象区域Y坐标。

  兼容性写法：e.client-this.offsetLeft。

## 方法

参考博客https://www.cnblogs.com/dcyd/p/12482989.html。

### preventDefault();

阻止默认动作

IE的兼容写法returnValue=false;

````js
if(event.preventDefault){   //兼容写法
    event.preventDefault();
}else{
    event.returnValue=false;
}
````

举个例子

````js
    document.getElementById("myform").onsubmit=function(e){
        e=e||window.event;
        var ss=document.getElementById("search").value;
        if(ss==""){
            document.getElementById("sss").innerHTML="请输入信息"
            e.preventDefault();  //阻止默认动作，如果满足条件不允许提交。
        }
    }
````

### stopPropagation();

阻止事件冒泡

IE的兼容写法cancelBubble=true;

#### 补充冒泡和捕获的概念

- 冒泡

　　° 就是从事件 目标 的事件处理函数开始，依次向外，直到 window 的事件处理函数触发

　　° 也就是从下向上的执行事件处理函数

- 捕获

　　° 就是从 window 的事件处理函数开始，依次向内，只要事件 目标 的事件处理函数执行

　　° 也就是从上向下的执行事件处理函数

````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<style>
    #con3{
        width: 100px;
        height: 100px;
        background-color: blue;
    }
    #con2{
        width: 200px;
        height: 200px;
        background-color: blueviolet
    }
    #con1{
        width: 300px;
        height: 300px;
        background-color: brown;
    }
</style>
<body>
    <div id="con1">
        <div id="con2">
            <div id="con3"></div>
        </div>
    </div>
</body>
<script>
    document.getElementById("con1").onclick=function(){
        alert(1)
    }
    document.getElementById("con2").onclick=function(){
        alert(2)
    }
    document.getElementById("con3").onclick=function(){
        alert(3)
    }
</script>
</html>
````

![image-20201229143405123](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201229143405123.png)

三层结构中，当到最里层时会依次弹出3,2,1，即执行为冒泡顺序。这里可以采用stopPropagation()的方法来阻止后面的冒泡

````js
 document.getElementById("con3").onclick=function(e){
        e=e||window.event;
        alert(3);
        e.stopPropagation();  //后面便不在冒泡，当点到3的时候只弹出3。
    }
````

## 事件委托

事件委托的原理：利用冒泡的原理，把事件加到父元素或者祖先元素上，触发效果。

​     1.提高性能和效率

2. 减少事件注册，节省内存占用

3. 未来元素无需再次注册事件

​     4.后面添加的元素也会有事件

`````js
    var list=document.getElementById("ulist");
    function clear(){
        for(i=0;i<list.children.length;i++){
            list.children[i].style.background="white";
        }
    }
    list.onclick=function(e){
        e=e||window.event;
        var nn=e.target.nodeName;
        if(nn=="LI"){     //其实是整个ul所包含的区域都会触发这个点击事件，这里的判定条件使li变色。
            clear();
            e.target.style.background="red";
        }
        // e.target.style.background="red";
    }
`````

![image-20201229151817327](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201229151817327.png)

点击到对应的地方才可以显示。