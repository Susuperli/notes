# 第六讲 jQuery中css基本属性处理

## css获取样式

- 获取样式的值（带单位）

  ```js
  $(this).css("width");  //获取生效的宽度，包括行内和css中，选择生效的，带单位
  ```

- 设置css样式

  ````js
  $(this).css("width","100px")
  ````

- 设置多个css样式

  ````js
  $(this).css({"color":"#0f0","fontSize":"30px"})
  ````

## jQuery中获得宽高的方法

- width()&&heigth()方法，获取的值不带单位。

  获取元素content的宽高

- innerHeight()和innerWidth()

  获取元素content+padding的宽高

- outerHeight()和outerWidth()

  获取元素content+padding+border的宽高

  - outerHeight(true)和outerWidth(true)

    获取元素content+padding+border+margin的宽高

## css位置属性处理

- offset()

  获取或设置当前元素的相对窗口的偏移量。

  $("p").offset().top;获取第一个p距离上边视口的距离。

  $("p").offset().left;获取第一个p距离左边边视口的距离。

  $("p").offset({"top":"40","left":"40"});设置偏移量。

- position()

  获取当前元素相对于最近的定位的偏移量。

- scrollTop()和scrolleft()

  获取或设置滚动条的位置。

  $("div:eq(0)").scrolllTop(); 获取滚动条的距离。

  $("div:eq(0)").scrolllTop(24); 设置滚动条的距离。

  ````html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>轮播图</title>
      <script src="../../jquery-3.5.1/jquery-3.5.1.min.js"></script>
  </head>
  <style>
      #show{
          width: 400px;
          height: 250px;
          overflow: hidden;
      }
      #content{
          width: 1600px;
          height: 250px;
      }
      #content>img{
          width: 400px;
          height: 250px;
      }
  </style>
  <body>
      <div id="show">
          <div id="content"><img src="picture/1.jpg"><img src="picture/2.jpg"><img src="picture/3.jpg"><img src="picture/4.jpg"></div>
      </div>
  </body>
  <script>
      $(document).ready(function(){
          function lbt(){
              $("#show").scrollLeft($("#show").scrollLeft()+20);
              if($("#show").scrollLeft()>=400){
                  $("#content").children().first().appendTo($("#content"));
                  $("#show").scrollLeft(0);
                  clearInterval(i);
                  start();
              }
          }
          function start(){
              setTimeout(function(){
                  i=setInterval(lbt,100)
              },1000);
          }
          start();
          // lbt();
      })  
  </script>
  </html>
  ````

  

  

