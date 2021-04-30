# 第十一讲 JavaScript的Dom和Bom对象——DOM对象

DOM文档对象模型Document Object Model：当前载入页面所拥有的对象（代表当前文档）。

## DOM特点

- 通过DOM可以对整个HTML文档进行新建、添加、更新、删除等操作。
- DOM模型符合WEB标准，兼容性好。
- 通过HTML可以操作HTML、XHTML、XML文档。

## DOM树

![u=4069710210,858097302&fm=26&gp=0](D:\0-Link\naotes\picture\u=4069710210,858097302&fm=26&gp=0.gif)

- 整个文档都是一个文档节点。
- 每个HTML都是一个元素节点。
- 包含在HTML元素中的文本是文本节点。
- 每一个HTML属性都是一个属性节点。
- 注释属于注释节点。

## Document对象获取文档元素

- 通过ID获取文档节点

  document.getElementById("id");

  `````js
  document.getElementById("transform");
  `````

- 通过name属性获取文档节点集合（伪数组）

  document.getElement**s**ByName("name")

  ````js
   var list=document.getElementsByName("one");//调用方法
      console.log(list);
      list[0].style.background="#f00";
      list.style.height="78px";
  ````

- 通过TagName标记名获取稳当点集合（伪数组）

  document.getElement**s**ByTagName("TagName")

  ````js
  var list=document.getElementsByTagName("li");
  console.log(list);
      list[0].style.background="#f00";  //调用方法
      list.style.height="78px";
  ````

- 通过ClassName标记名称获取文档集合（数组）

  document.getElement**s**ByClassName("ClassName")

  ````js
   var list=document.getElementsByClassName("one");   //ClassName方法
      console.log(list);
      list[1].style.background="#f00";
      list.style.height="78px";
  ````

- document.querySelector()

  css选择符模式，返回该模式匹配的第一个元素，结果为一个元素，如果找不到则会返回null。

  ````html
   <li class="one"></li>
          <li></li>
          <li></li>
          <li></li>
          <li class="one"></li>
  ````

  ````js
  var list=document.querySelector(".one");     //querySelector方法
      
      console.log(list);
      list.style.background="#f00";
      list.style.height="78px";
  ````

  ![image-20201222140822187](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201222140822187.png)

  **注：该方法只是会匹配到第一个样式，即使有两个one类；要使用 .one类似css中的选择器。**

- document.querySelectorAll()

  `````js
  var list=document.querySelectorAll(".one");
  
      console.log(list);
      list[0].style.background="#f00";
      list.style.height="78px";
  `````

  该方法也会是生成一个伪数组，也需要下标的方式来找到你想要的。

## 文本节点的处理

- **innerText**

  ````html
  <ul>
          <li id="one">
              <div>
                  hello world
              </div>
          </li>
          <li></li>
          <li></li>
          <li></li>
          <li class="one"></li>
    </ul>
  ````

  获取或设置元素文本内容

  ````js
  var i=document.getElementById("one").innerText;
      console.log(i);
  ````

  ![image-20201222143334689](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201222143334689.png)

- textContent

  获取或设置元素文本内容。

- **innerHTML**

  获取或设置元素中**所有内容**，包括HTML代码

  ![image-20201222143455388](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201222143455388.png)

  **注：主要区别和innerText的区别。**

### 节点信息

每个节点都拥有包含着关于节点某些信息的属性。这些属性是：

- nodeName（节点名称）
- nodeValue（节点值）
- nodeType（节点类型）

#### nodeName

nodeName 属性含有某个节点的名称。

- 元素节点的 nodeName 是标签名称
- 属性节点的 nodeName 是属性名称
- 文本节点的 nodeName 永远是 #text
- 文档节点的 nodeName 永远是 #document

注释：nodeName 所包含的 XML 元素的标签名称永远是大写的

#### nodeValue

对于文本节点，nodeValue 属性包含文本。

对于属性节点，nodeValue 属性包含属性值。

nodeValue 属性对于文档节点和元素节点是不可用的。

#### nodeType

nodeType 属性可返回节点的类型。

最重要的节点类型是：

| 元素类型 | 节点类型 |
| :------- | :------- |
| 元素     | 1        |
| 属性     | 2        |
| 文本     | 3        |
| 注释     | 8        |
| 文档     | 9        |

## Document对象操纵节点

### 创建节点

document.createElement();创建一个节点。

document.createTextNode()；创建一个文本节点。

`````js
var aaaa=document.createElement("div");
    // aaaa.innerHTML="你好";    //写入方法1
    var bbbb=document.createTextNode("你好")   //写入方法2
`````

### 添加节点

- appendChild(node);

  添加节点到当前文本节点内部的后面（**新创建的接点**）。

  ````js
  var aaaa=document.createElement("div");
      // aaaa.innerHTML="你好";    //写入方法1
      var bbbb=document.createTextNode("你好")   //写入方法2
      var cccc=aaaa.appendChild(bbbb);                  //写入方法2
      console.log(aaaa);
      var one=document.getElementById("one");
      one.appendChild(cccc);
  ````

  移动节点到当前节点内部的后面（对于已有节点可进行移动的操作）。

  ````html
  <!DOCTYPE html>
  <html>
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <body>
      <h3 id="link" onclick="move()">朗科</h3>
      <div id="one">
          <h1>sad</h1>
      </div>
  </body>
  <script>
     function move(){     //appendChild移动方法
         var h=document.getElementById("link");
         document.getElementById("one").appendChild(h);
     }
  </script>
  </html>
  ````

  点击文字便可以完成移动的操作。

  ![image-20201223203620445](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201223203620445.png)![image-20201223203637880](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201223203637880.png)

  其实都可以理解为移动，区别是一个移动的是内存中的变量，看起来像是“添加”；另一个则是移动已有的变量。

- insertBefore

  insertBefore(要移动的节点,参考节点)

  添加节点到当前节点内部的参考节点的前面。

  移动节点到当前节点内部的参考节点的前面。

  ````html
  <!DOCTYPE html>
  <html>
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <body>
      <h3 id="link" onclick="move()">朗科</h3>
      <div id="one">
          <h1>sad</h1>
      </div>
  </body>
  <script>
     function move(){     //insertBefore方法移动
         var h=document.getElementById("link");
         document.getElementById("one").insertBefore(h,document.getElementsByTagName("h1")[0]);
     }
  </script>
  </html>
  ````

### 删除节点

- remove()

  删除当前节点（IE不兼容，pc端不常用，但是移动端可以用）

  ````js
  document.getElementById("link").remove();
  ````

- removeChild(要删除的节点)

  删除当前节点的子节点node。

  ````js
   document.getElementsByTagName("body")[0].removeChild(document.getElementById("link"));//删除body节点中的某一节点
  ````

### 复制接点

- cloneNode(true);

  深拷贝——除了复制节点，还复制所有节点及其文本。

- cloneNode(false);

  浅拷贝——复制节点。

````html
<!DOCTYPE html>
<html>
    <body>

        <ul id="myList1"><li>Coffee</li><li>Tea</li></ul>
        <ul id="myList2"><li>Water</li><li>Milk</li></ul>

        <p id="demo">请点击按钮把项目从一个列表复制到另一个列表中。</p>

        <button onclick="myFunction()">试一下</button>

        <script>
                function myFunction(){
                    var itm=document.getElementById("myList2").lastChild;
                    var cln=itm.cloneNode(true);           //改成false只是会复制其空标记
                    document.getElementById("myList1").appendChild(cln);
                }
        </script>
    </body>
</html>
````

![image-20201223212537076](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201223212537076.png)

![image-20201223212605555](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201223212605555.png)

false情况

![image-20201223212639978](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201223212639978.png)

### 替换节点

- replaceChild(新节点,被替换的节点)

  移动原有的节点来替换指定节点

  ```html
  <!DOCTYPE html>
  <html>
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <body>
      <h3 id="link" onclick="move()">朗科</h3>
      <div id="one">
          <h1>sad</h1>
      </div>
  </body>
  <script>
      //替换
     function move(){     
         var h3=document.getElementById("link");
         var h1=document.getElementsByTagName("h1")[0];
       
         document.getElementById("one").replaceChild(h3,h1);
     }
  </script>
  </html>
  ```

  创建新节点来替代指定节点

### 判断节点是否有子节点

返回值是布尔型。

````html
<!DOCTYPE html>
<html>
        <head>
                <meta charset="utf-8">
                <title></title>
        </head>
        <body>

                <ul id="myList"><li>Coffee</li><li>Tea</li></ul>
                <p id="demo">单击按钮是否有任何子节点列表元素</p>
                <button onclick="myFunction()">点我</button>
                <script>
                        function myFunction(){
                                var lst=document.getElementById("myList");
                                var x=document.getElementById("demo");
                                x.innerHTML=lst.hasChildNodes();
                        }
                </script>
                <p><strong>注意:</strong>空格内节点被认为是文本节点,所以如果你留下任何空格或换行一个元素,该元素仍有子节点。 </p>

        </body>
</html>
````

注：**这里需要注意的是，空格算是文本节点**，返回值是布尔型。

### 是否包含某节点

## document访问相关节点（属性）

### 更改为父节点

-parentNode 更改对象为当前节点的父节点。

```js
 var t=document.getElementById("two");
    t.style.background="#0f0";
    t.parentNode.style.border="1px solid #000"
```

### 通过父元素更改为子元素

- firstChild 

  更改为当前对象的第一个子节点,**前面不能有空格，否则获取的是空格这个文本节点。**

  ```html
  <!DOCTYPE html>
  <html>
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <body>
     <div id="con"><p>son1</p>             <!--注意此处结构-->
      <p id="two1">son2</p>
      <p>son3</p>
  </div>
  </body>
  <script>
     var a=document.getElementById("con");
     a.style.background="red";
     a.firstChild.style.border="1px solid black";
  </script>
  </html>
  
  ```

- lastChild

  同firstChild，不能有空格。

- firstElementChild

  返回值是第一字元素子节点，允许有空格（IE9以下不支持）。

- lastElementChild

  返回值是最后一个子元素节点，允许有空格（IE9以下不支持）。

- 以集合的方式更改为子节点

  参考https://blog.csdn.net/look55/article/details/51088407

  childNodes更改为子元素的集合（下标从0开始）。

  children更改为子元素的集合（下标从0开始）。

  区别

  - `childNodes`属性返回所有的节点，包括文本节点、注释节点；

  - `children`属性只返回元素节点；

    ````html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <ul id="ul">
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </body>
    <script>
        // var son=document.getElementById("ul").childNodes;
        // for(var i=0;i<son.length;i++){
        //     console.log(son[i]);
        // }
        var son2=document.getElementById("ul").children;
        for(var j=0;j<son2.length;j++){
            console.log(son2[j]);
        }
    </script>
    </html>
    ````

    ![image-20201223224750452](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201223224750452.png)

    ![image-20201223224818503](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201223224818503.png)

### 更改为兄弟节点

- nextSibling

  下一个兄弟节点。**不能有空格。**

- previousSibling

  上一个兄弟节点。**不能有空格。**

- nextElementSibling

  下一个兄弟元素节点。

- previousElementSibling

  上一个兄弟元素节点。

## 元素的属性设置

- getAttribute("属性名");

  获得属性节点

- setAttribute("属性名","值")

  设置节点属性

  `````html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
  </head>
  <style>
      .con{
          width: 100px;
          height: 100px;
          background-color: red;
          margin: 50px 0 0 100px;
          transition: transform 300ms;
      }
      .cons{
          transform: scale(2,2);
      }
  </style>
  <body>
      <div id="con" class="con" onclick="scale()"></div>
  </body>
  <script>
      function scale(){
          var con=document.getElementById("con")
          if(con.getAttribute("class")=="con"){
              con.setAttribute("class","con cons")     //前面是要更改的属性，后面是要更改为的属性值
          }else{
          con.setAttribute("class","con")
          }
      }
  </script>
  </html>
  `````

- removeAttribute("属性名")

  删除属性节点。

- style.cssText

  获取或者设置行内模式的样式

  注：如font-size改成fontSize的驼峰命名法。
  
- className

  应用选择器class=类名。

  
  
  
  
  
  
  



