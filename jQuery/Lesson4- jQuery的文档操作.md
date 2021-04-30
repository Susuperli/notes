# 第四讲 jQuery的文档操作

## 移动元素

- append();

  向每个匹配的的元素**末尾追**加内容，$("选择器1").append("选择器2")。会将匹配的2移动到1中。

  `````js
  <!DOCTYPE html>
  <html>
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
      <script src="../../jquery-3.5.1/jquery-3.5.1.min.js"></script>
  </head>
  <style>
      div{
          border: black solid 1px;
          width: 200px;
          height: 200px;
      }
  </style>
  <body>
      <button id="btn">点我</button>
      <div id="con"></div>
      <h1>你好</h1>
  </body>
  <script>
      $(document).ready(function(){
          $("#btn").click(function(){
              //append方法
              $("#con").append("<h1>hi!</h1>")   //可以直接写出标记
              // $("#con").append($("h1"))  //移动在括号里面可以写标记选择器
              //appendTo方法
              $("h1").appendTo($("#con"));
          })
      })
  </script>
  </html>
  `````

  对于append()方法，可以直接写标记选择器，也可以选择直接在方法内部写出标记形状。

- appendTo();

  与append方法相反，A to B，把a放进b中。

- prepend()

  向每个元素的**前面**添加元素。

  ````js
  $("#con").prepend($("h1"));
  ````

- prependTo()

  同appendTo()。

- after()

  在每个匹配到的元素之后插入内容

  ````js
  $("#ss").after($("h1"))
  ````

- insertAfter();

  将所有的匹配元素插入到指定元素的后面。

  ````js
  $("h1").insertAfter($("#ss"))
  ````

- before()

  在每个匹配到的元素之前插入内容

- insertBefore()

  将所有的匹配元素插入到指定元素的前面。

## 复制元素

- clone()

  clone() 方法生成被选元素的副本，包含子节点、文本和属性。可选参数true和false，默认为false表示所复制的内容不包括绑定事件；true表示包括绑定事件。

  `````js
   $("body").append($("p").clone());
  `````

## 替换元素

- replaceWith()

  replaceWith() 方法把被选元素替换为新的内容。

  ````js
  $("p").replaceWith("<b>Hello world!</b>");
  ````

  用后面的内容代替前面的内容。

- replaceAll()

  replaceAll() 方法把被选元素替换为新的 HTML 元素。

  ````html
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="utf-8">
  <title></title>
  <script src="../../jquery-3.5.1/jquery-3.5.1.min.js"></script>
  <script>
  $(document).ready(function(){
  	$("button").click(function(){
  		$("<span><b>Hello world!</b></span>").replaceAll("p:last");
  	});
  });
  </script>
  </head>
  <body>
  
  <button>用一个span元素替换最后一个p元素</button><br>
  <p>这是一个段落。</p>
  <p>这是另一个段落。</p>
  
  </body>
  </html>
  ````

  ![image-20210111221400947](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210111221400947.png)

  ![image-20210111221417370](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210111221417370.png)

## 包裹元素

所谓包裹元素就是对某元素的父元素进行操作。

- wrap()

  wrap() 方法使用指定的 HTML 元素来包裹每个被选元素。同时也可以**复制页面**上原有的元素来包裹当前被选中的页面元素。

  ````html
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="utf-8">
  <title></title>
  <script src="../../jquery-3.5.1/jquery-3.5.1.min.js"></script>
  <script>
  $(document).ready(function(){
  	$("button").click(function(){
  		$("#one").wrap($("#two"));
  	});
  });
  </script>
  <style type="text/css">
  div{background-color:yellow;}
  </style>
  </head>
  <body>
  
  <p id="two">这是一个段落。</p>
  <p id="one">这是另一个段落。</p>
  <button>给每个P元素包裹一个div元素</button>
  
  </body>
  </html>
  ````

- unwrap()

  **删除**当前元素的父元素。

## 删除和清空元素

- remove()

  删除当前元素，该元素所包括的文本内容和后代元素同时删除。

  可以将删除的元素移动到其他位置，但是事件不会保留。

  ````html
  <html>
  <head>
  <script type="text/javascript" src="/jquery/jquery.js"></script>
  <script src="../../jquery-3.5.1/jquery-3.5.1.min.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){
    $("button").click(function(){
      $("body").append($("p").remove());    //把要删除的元素移动到body里面，但是不会保留事件。
    });
  });
  </script>
  </head>
  <body>
  <p>This is a paragraph.</p>
  <button>移动 p 元素</button>
  </body>
  </html>
  ````

- detach()

  删除当前元素，该元素所包括的文本内容和后代元素同时删除。

  可以将删除的元素移动到其他位置，但是事件会保留。

  ````html
  <html>
  <head>
  <script type="text/javascript" src="/jquery/jquery.js"></script>
  <script src="../../jquery-3.5.1/jquery-3.5.1.min.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){
    $("button").click(function(){
      $("body").append($("p").detach());
    });
   $("p").click(function(){
      $(this).animate({fontSize:"+=1px"})
    });
  });
  </script>
  </head>
  <body>
  <p>在本段落移动之后，试着点击该段落，请注意它保留了 click 事件。</p>
  <button>移动 p 元素</button>
  </body>
  </html>
  ````

  移动了元素且保留了自身的事件。

- empty()

  empty() 方法移除被选元素的所有子节点和内容。

  **注意：**该方法**不会移除元素本身**，或它的属性。

  **提示：**如需移除元素，但保留数据和事件，请使用 [detach()](https://www.runoob.com/jquery/html-detach.html) 方法。

  **提示：**如需移除元素及它的数据和事件，请使用 [remove()](https://www.runoob.com/jquery/html-remove.html) 方法。

