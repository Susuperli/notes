# 第五讲 元素的属性处理

## attr()方法

获取某元素某个属性值，或者是设置一个参数值。

```js
$(secetor).attr("aattr","value");
```

````html
<body>
    <div class="one" style="border: cornflowerblue 1px solid;"></div>
</body>
<script>
    $(document).ready(function(){
        var a=$(".one").attr("style");  //获取属性值
        console.log(a);
    })
</script>
````

![image-20210111162427243](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210111162427243.png)

## removeAttr()

删除指定的属性

````js
$("div").removeAttr("class");  //删除其所有的类名
````

## 元素的class属性处理

- addClass()

  可以给元素增加额外的类名。

  ````js
  $(document).ready(function(){
          $("div").click(function(){
              $(this).addClass("two");  //为你的div增加一个新的类
          })
      })
  ````

- removeClass()

  移除一个元素的class的**属性值**

- toggleClass()

  切换class属性中一个或者多个属性值，该方法检查每个元素中指定的类。如果不存在则添加类，如果已设置则删除之。这就是所谓的切换效果。

  ````html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
      <script src="../../jquery-3.5.1/jquery-3.5.1.min.js"></script>
  </head>
  <style>
      .one{
          width: 100px;
          height: 100px;
          background: black;
      }
      .two{
          background-color: brown;
      }
  </style>
  <script>
      $(document).ready(function(){
          $("div").click(function(){
              $("div").toggleClass("two");
           })
      })
  </script>
  <body>
      <div class="one">
  
      </div>
  </body>
  </html>
  ````

  **使用function给toggle添加转换条件**

  ````html
  <html>
  <head>
  <!-- <script type="text/javascript" src="/jquery/jquery.js"></script> -->
  <script src="../../jquery-3.5.1/jquery-3.5.1.min.js"></script>
  <script type="text/javascript">
  $(document).ready(function(){
    $("button").click(function(){
      $('ul li').toggleClass(function(){
          console.log($(this).index())
        return 'listitem_' + $(this).index();
      });
    });
  });
  </script>
      <style type="text/css">
          .listitem_1, .listitem_3
          {
          color:red;
          }
          .listitem_0, .listitem_2
          {
          color:blue;
          }
      </style>
  </head>
  
  <body>
      <h1 id="h1">This is a heading</h1>
      <ul>
          <li>Apple</li>
          <li>IBM</li>
          <li>Microsoft</li>
          <li>Google</li>
      </ul>
      <button class="btn1">添加或移除列表项的类</button>
  </body>
  </html>
  ````

- hasClass()

  判断是否含有某个类，返回值为一个布尔型，是为true，否为false。

## 获取文本文档

- html()
- text()

