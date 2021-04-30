# 第九讲 jQuery其他对象的处理

一、对元素进行遍历操作

1.如果要遍历一个jquery对象，对其中每个匹配元素进行相应处理，那么可以使用each()方法。

　　$("div").each(function(index,element){

　　　　$(this).css("border":"6px solid black");

　　})

````js
<html>
<head>
<script type="text/javascript" src="/jquery/jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $("button").click(function(){
    $("li").each(function(){
      alert($(this).text())
    });
  });
});
</script>
</head>
<body>
<button>输出每个列表项的值</button>
<ul>
<li>Coffee</li>
<li>Milk</li>
<li>Soda</li>
</ul>
</body>
</html>
````

2.增加判断条件

　　$("div").each(function(index){

　　　　if(index!=2&&index<5)

　　　　$(this).css("border","6px solid black");

　　})

3.执行each()方法里面的函数时，如果返回false，则停止循环，效果等价于javascript中的break；如果返还true，则直接进入下一个循环，等价于javascript中的contiune；

　　$("div").each(function(index){

　　　　if(index==2) return true;

　　　　if(index==5) return false;

　　　　$(this).css("border","6px solid black");

　　})

4.对元素进行数据存取

　　1.将数据存储在文本里面

　　

```js
var` `flag=``true``；<br>$(``"#btn1"``).click(``function``(){<br>　　``if``(flag){<br>　　　　$(``"p"``).text(``"true"``);<br>　　　　flag==``false``;<br>　　}``else``{<br>　　　　$(``"p"``).text(``"false"``);<br>　　　　flag=``true``;<br>　　}<br>})
```

　　2.在元素上存储数据

　　　将数据存储在元素的属性里面

```js
$(``"p"``).attr(``"alt"``,``"false"``);<br>$(``"#btn2"``).click(``function``(){<br>　　``if``($(``"p"``).attr(``"alt"``)==``"true"``){<br>　　　　$(``"p"``).text(``"true"``).attr(``"alt"``,``"false"``);<br>　　}``else``{<br>　　　　$(``"p"``).text(``"false"``).attr(``"alt"``,``"true"``);<br>　　}<br>})
```

　　 3.将数据存储在元素data方法的参数中

　　语法：data("变量名"，变量值)；

```js
$(``"p"``).data(``"flag"``,``false``);<br>$(``"#btn2"``).click(``function``(){<br>　　``if``($(``"p"``).data(``"flag"``)){<br>　　　　$(``"p"``).text(``"true"``).data(``"flag"``,``false``);<br>　　}``else``{<br>　　　　$(``"p"``).text(``"false"``).data(``"flag"``,``true``);<br>　　}<br>})
```

　　　4.克隆元素同时克隆数据

　　方法：clone():不带参数，值复制元素，不会复制元素上绑定的事件和数据。

　　　　　clone(true)方法：复制元素的同时，复制元素上绑定的事件和数据。

　　　　

```js
$(``"p:first"``).clone().insertAfter($(``"p:eq(0)"``));<br>$(``"p:first"``).clone(``true``).insertAfter($(``"p:eq(1)"``));<br>alert($(``"p:eq(1)"``).data(``"test1"``));``//undefined<br>alert($("p:eq(2)").data("test1"));//true
```

　　　5.清除附加在元素上的变量：removeData()

　　

```js
$(``"p"``).data(``"test1"``,``true``).data(``"test2"``,{first:1,last:``"two"``});<br>创建变量test1，且复制为``true``；创建变量test2且赋值为{first:1,last:``"two"``};<br>$(``"p"``).removeData(``"test1"``);<br>alert($(``"p"``).data(``"test1"``));输出为undefined<br>alert($(``"p"``).data(``"test2"``).first)；``//1<br>alert($("p").data("test2").last);//two<br>如果要清楚元素上的全部变量使用removeData()不带参数，等价的方法有remove()和empty()方法。
```

二、元素的个数和索引

1.size()方法：计算jq对象中的元素的个数

　　--length()

2.index()方法：返回某个元素相对于其他兄弟元素的索引位置

　index()不带参数，他会计算第一个匹配选择器的元素的相对于其他兄弟的索引位置

　　$("#core").index();