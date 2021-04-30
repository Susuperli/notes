# 第三讲 盒子模型

## 盒子模型

### 概念

​        所有页面的元素都可以看成一个盒子，占据着一定的页面空间。一般来说，这些被占据的空间都要比单纯的空间要大，我们可以通过调节边框和属性参数的方法来调整这些盒子大小。

### 属性及其属性值

- content：**在style中可以是通过控制width&height的大小来控制content内容的大小。**

  ````html
  <!DOCTYPE html>
  <html>
  	<head>
  		<meta charset="utf-8">
  		<title></title>
  		<style>
  			div{
  				width:200px;
  				height:200px;
  			}
  		</style>
  	</head>
  	<body>
  		<div>
  		hello world
          </div>
  	</body>
  </html>
  ````

  如上，可以设置宽高对content内容作出限制。在浏览器中可通过F12的开发者选项来看到content的实际大小。

- border边框

  属性主要有三种，color（颜色）、width（粗细）、style（样式）。

  color：支持所有的写入方法，#f00，red，rgb（）。

  width：粗细，单位是px。

  style：边框线的风格，包含有**none（默认）**、hidden、**dotted（圆点虚线）、dashed（线条虚线）、solid（实线）、double（双实线）**、groove、ridge、inset、outset。加粗内容为常用内容。

  ````html
  <style>
      div{
         border-style:solid;
  	border-color:red;
  	border-width:5px;
  	padding-left:20px;                    
      }
  </style>
  或者
  <style>
      border:20px red solid;
  </style>
  ````
  

可以使用边框设置类似小三角的图案，代码如下所示：

````html
  <style>
      div{
          width:0px;
          height:0px;
          border:10px solid transparent;
          border-left:10px solid green;
      }
  </style>
````

效果如下：

![image-20201108133111855](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201108133111855.png)

- padding内边距

  用于控制content与border的距离。使用方法与border类似也可以单独设置上右下左的距离。

  padding:20px;表示全部距离。padding:20px 10px;分别表示上下左右的距离。

  padding:20px 10px 5px；分别表示上、左右、下的距离。padding:20px 1px 1px 1px;分别表示上右下左的距离。

- margin

  两个块级元素上下之间的距离，是上面的盒子的margin-bottom和下面盒子margin-top之间的最大值。

  **而对于行内元素，不能控制其大小即上下距离但是左右的距离是可以控制的，其值是左边的margin-right和右边元素的margin-left之和。**

### 盒子实际宽度的算法

对于标准的盒子其宽度为：**content+padding-left&right+border-left&right+margin-left&right。**

### 非标准盒子和标准盒子之间的区别

对于IE8及其以下版本IE浏览器属于非标准的盒子模型（现在已不需要考虑，但是需要了解）

其width&height指的是content+padding+border的大小。

## 补充内容

### 行内元素和块级元素

|              块级元素              |                      行内元素                      |
| :--------------------------------: | :------------------------------------------------: |
|         总是从新的一行开始         |                和其他元素都在一行上                |
|         高度、宽度是可控的         | 高度、宽度以及外边框（上下不可控，左右可控）不可控 |
|  宽度缺省时，它的容器宽度是100％   |      宽度就是他的文字或是图片的高度，不可改变      |
| 块级元素可以包括块级元素和行内元素 |              行内元素只能包括行内元素              |

### 行内元素与块级元素的转换

display：block|inline|inline-block|table-cell|none

block：行内转换为块级。

inline：行内转换为块级。

inline-block：行内块级，对于行内使用，几乎不对块级使用，使用时可以设置其大小。

table-cell：转换为表格单元格的渲染模型。

none：隐藏元素。

### 盒子转换

**box-sizing** 属性用来改变默认的 CSS盒模型 对元素宽高的计算方式。这个属性可以用于模拟那些非正确支持标准盒模型的浏览器的表现。

**box-sizing**：content-box（default） | border-box ;

**content-box**

　　　　默认值，标准盒模型。 width与 height 只包括内容的宽和高， 不包括边框（border），内边距（padding），外边距（margin）。

　　　　注意: 内边距, 边框 & 外边距 都在这个盒子的外部。

　　　　比如. 如果 .box {width: 350px}; 而且 {border: 10px solid black;} 那么在浏览器中的渲染的实际宽度将是370px;


　　　　*尺寸计算公式：width = 内容的宽度，height = 内容的高度。宽度和高度都不包含内容的边框（border）和内边距（padding）。*

**border-box** 

　　　　width 与 height 包括内边距（padding）与边框（border），不包括外边距（margin）。

　　　　这是IE 怪异模式（Quirks mode）使用的 盒模型 。注意：这个时候内边距和边框将会包括在盒子中。

### 圆角边框设置

border-radius:nth;可以设置圆角的大小。

四个值表示：左上、右上、右下、左下；

三个值表示：左上、右上左下、右下；

两个值：左上右下、右上左下；

一个值：表示四个角。

### 边界图片



