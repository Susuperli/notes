# 第十一讲 jQuery插件的封装

## 第一类插件扩展，jQuery的方法

- 结构

  ````js
  $.funName=function(参数){
      代码块；
  }
  
  //调用方法
  $.funName(参数)
  ````

  ![jq10举例](D:\0-Link\naotes\picture\jq10举例.png)

  ````js
  $.extend({
      funName1:function(参数){
          代码块;
      },  //注意逗号","
      funName2:function(参数){
          代码块;
      },
      ....
  })
  //调用方法相同
  $.funName(参数);
  ````

  ![jq10举例2](D:\0-Link\naotes\picture\jq10举例2.png)

- 

## 第二类插件扩展，jQuery对象的方法

`````js
$.fn.funName=function(参数){
    代码块;
}
//调用
object.funName(参数);
`````

````js
$.fn.extend(){
    nac:function(){
        reture this.each(function(){//返回代用该方式时对象的集合
            代码块;
        })
    }
    sajdk:function(){
        代码块;
    }
}
````

## css3特效

animationcss插件

![css3特效](D:\0-Link\naotes\picture\css3特效.png)

````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>animationcss</title>
    <link rel="stylesheet" href="../../animationcss插件/animate.min.css">
    <style>
        div{
            font-size: 32px;
            display: none;
        }
        .aa{
            display: block;
        }
    </style>
</head>
<body>
    <button id="btn">click me</button>
    <div id="con" class="">你好啊</div>
</body>
<script>
    document.getElementById("btn").onclick=function(){
        if(document.getElementById("con").className==""){
            document.getElementById("con").className="bounceIn animated aa";
        }else{
            document.getElementById("con").className="";
        }
        
    }
</script>
</html>
````

