# 第七讲 jQuery对象的动画处理

## 隐藏显示

- hide()

  动态改变当前匹配对象的宽、高、透明度，最终会隐藏该元素，即display成为none；

  参数可以是时间，默认是0，单位是毫秒，也可以是slow(0.6s),normal(0.4s),fast(0.2s)。

  ![image-20210112150951976](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210112150951976.png)

- show()

  动态改变当前匹配对象的宽、高、透明度，最终会隐藏该元素，即display成为none以外的属性值；

  参数可以是时间，默认是0，单位是毫秒，也可以是slow(0.6s),normal(0.4s),fast(0.2s)。

- toggle()

  动态改变当前匹配对象的宽、高、透明度，在可见和不可见的状态之间进行切换。

  ````js
  $(selector).toggle(speed,easing,callback)
  ````

  | 参数       | 描述                                                         |
  | :--------- | :----------------------------------------------------------- |
  | *speed*    | 可选。规定隐藏/显示效果的速度。可能的值：毫秒"slow""fast"    |
  | *easing*   | 可选。规定在动画的不同点上元素的速度。默认值为 "swing"。可能的值："swing" - 在开头/结尾移动慢，在中间移动快"linear" - 匀速移动**提示：**扩展插件中提供更多可用的 easing 函数。 |
  | *callback* | 可选。toggle() 方法执行完之后，要执行的函数。如需学习更多有关 callback 的内容。 |

## 浅入浅出

- fadeOut()

  动态的改变当前元素的不透明度，(其他的并无变化)最终会隐藏该元素，此时元素的css样式为none，语法结构与hide()和show()相同。

- fadeIn()

  动态的改变当前元素的不透明度，(其他的并无变化)最终会显示该元素，此时元素的css样式为none，语法结构与hide()和show()相同。

- fadeToggle()

  动态显示隐藏

- fadeTo()

  动态调整到指定的不透明度，fadeTo(time,opaction)

  ````js
   $("div").fadeTo(1000,0.5);
  ````


- slideUp()&&slideDown()&&slideToggle()

  隐藏&&显示&&切换

  二级菜单

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
          *{
              padding: 0;
              margin: 0;
          }
          ul{
              list-style-type: none;
          }
          .aa{
              width: 1000px;
          }
          .aa>li{
              width: 200px;
              float: left;
              text-align: center;
              background-color: blueviolet;
          }
          .aa>li>ul{
              background-color: coral;
              display: none;
          }
      </style>
      <script>
          $(document).ready(function(){
              $(".aa").children("li").mouseenter(function(){  //鼠标事件的区别
                  $(this).children("ul").slideDown(500);
              }).mouseleave(function(){
                  $(this).children("ul").slideUp(500);
              })
          })
      </script>
      <body>
         <ul class="aa">
             <li>手机
                 <ul>
                     <li>华为</li>
                     <li>小米</li>
                     <li>苹果</li>
                 </ul>
             </li>
             <li>
              手机
                  <ul>
                      <li>华为</li>
                      <li>小米</li>
                      <li>苹果</li>
                  </ul>
             </li>
             <li>
                  手机
                  <ul>
                      <li>华为</li>
                      <li>小米</li>
                      <li>苹果</li>
                  </ul>
             </li>
             <li>
                  手机
                  <ul>
                      <li>华为</li>
                      <li>小米</li>
                      <li>苹果</li>
                  </ul>
             </li>
             <li>
                  手机
                  <ul>
                      <li>华为</li>
                      <li>小米</li>
                      <li>苹果</li>
                  </ul>
             </li>
         </ul> 
      </body>
      </html>
  ````

  

## 动画效果

### animate()

animate() 方法执行 CSS 属性集的自定义动画。

该方法通过 CSS 样式将元素从一个状态改变为另一个状态。CSS属性值是逐渐改变的，这样就可以创建动画效果。

只有数字值可创建动画（比如 "margin:30px"）。字符串值无法创建动画（比如 "background-color:red"）。

animate({"样式名":"值"},time);，可以使元素运动到不同的位置，不过必须是确保元素的css属性position已经被设为absolute、relative、fixed。

- 增量

  $("p").animate({"marginTop":"+=300px"}),每次点击都移动300px。

### 动画队列

````js
$("p").animate({}).animate({})   //执行为动画1才会执行动画2。
````

````js
$(".start").click(function(){
             $("div").animate({"left":"500px"},3000).animate({"top":"500px"},3000).animate({"left":"0px"},3000).animate({"top":"0px"},3000)
        }) 
````

### 延迟动画

延迟动画队列，如果需要延迟执行当前元素的某个效果，可以使用delay()方法。放在要执行的动画之前，单位毫秒。

`````js
$("div").delay(1200).animate({height:"900px"})
`````

###  终止动画队列

stop(接下来尚未执行完的动画队列是否要清空,是否直接将正在执行的动画调到末状态)两个参数的默认都是false。

### 回调函数

animate({},time,callback)

