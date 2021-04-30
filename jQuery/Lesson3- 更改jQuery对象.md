# 第三讲 更改jQuery对象

## 更改为后代

- children();

  children("选择器") 选择子元素中，所有匹配选择器的子元素。

  children()/children("*") 选择父元素中所有的子元素。

- find();

  find("选择器") 选择后代中所有匹配的元素，括号里面不写就搜索不到东西。

- contents(); 选择文本和子元素。

## 更改为祖先元素

- parent("选择器") 

  选择父元素，所有匹配的父元素，不写选择器则选择所有父元素。

- parents()

  有选择器是选择符合条件的祖先元素，没有选择器则是选择所有祖先元素知道html。

- parentsUntil()

  有选择器则是到符合条件的祖先元素，直到型，没有选择器则是同上一个。

- offsetParent()

  选择最近的定位的祖先元祖，且该元素的css属性display不能为none。

- closest()

  选择器是选择本身或是或其祖先元素中符合条件的元素。

## 更改为找兄弟

- next()&prev()

  只选择上一个或者是下一个，如果选择器不匹配则是不选择中元素。

- nextAll(),prevAll(),sibling()

  选择向上或是向下的或者所有的兄弟元素。

## 更改为更多元素

- add()

  在原先的元素基础上添加

- andself()

  已删除

## 更改为部分元素的集合

- eq(),first(),last()

  获取当前对象中指定索引所对应的的元素，前面要有对象。first()=eq(0)。

  ````js
   $(document).ready(function(){
      $(".two").eq(1).css("border","1px solid red");
      })
  ````

- slice()

  包括开始，不包括结束。

- filter()和not()

  filter(),选择有选择器的

  not(),选择没有选择器的

- has()

  has() 方法返回拥有匹配指定选择器的一个或多个元素在其内的所有元素。

  ````html
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="utf-8">
  <title>菜鸟教程(runoob.com)</title>
  <script src="https://cdn.staticfile.org/jquery/1.10.2/jquery.min.js">
  </script>
  <script>
  $(document).ready(function(){
    $("p").has("span").css("background-color","yellow");
  });
  </script>
  </head>
  <body>
  
  <h1>欢迎来到我的主页</h1>
  <p>我的<span>名字</span>叫 Donald。</p>
  <p>我住在<span>Duckburg</span>。</p>
  <p>我最好的朋友是 Mickey。</p>
  
  </body>
  </html>
  ````

  ![image-20210107094439755](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210107094439755.png)

## 还原jQuery对象的方法

- end()方法返回上一个的操作对象

