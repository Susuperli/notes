# 第十讲 框架（H5中备废除）

## 基本结构

### 简介

​        框架可以将浏览器分隔成多个小窗口，并且在每个小窗口中可以显示不同的网页，这样我们就可以很方便的浏览不同的网页效果图。当网页被分隔成多个窗口后，各个窗口就会扮演不同的角色，实现不同的功能。举例来说，有些论坛就会把网页分割成两个窗口，一个主要用来显示帖子的标题，而另一个窗口会显示具体内容，这样的设计显然比起来个窗口的网页来说，在浏览时方便的多，而且还可以任意切换题目。

### 结构

- 基本结构

  框架的基本结构主要分为框架和框架集两个部分。利用\<frame>标记，\<frameset>标记来定义。其中\<frame>标记用于定义框架，而\<frameset>标记则用于定义框架集。会代替\<body>的位置。

  ````html
  <!doctype html>
  <HTML>
      <head>
          <title>练习主页</title>
      </head>
      <frameset>
          <frame src="url">
          <frame src="url">
          <frame src="url">
          <frame src="url">
      </frameset>
  </HTML>
  
  ````

- 水平分割

  rows="高度1，高度2，...，*"

  可以设置水平分割的高度，可以用像素也可以用百分比表示，不同的高度的之间用“，”隔开，剩下的可以用*表示所有剩下的所有。

  ````html
  <frameset rows="300,200,*">
      <frame src="https://baidu.com"></frame>
      <frame src="https://lol.qq.com"></frame>
      <frame src="https://www.sina.com.cn"></frame>
  </frameset>
  
  ````

  ![image-20201105152151504](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201105152151504.png)

- 垂直分割

  与水平分割类似，只是将rows改为cols其他用法一样

  cols="高度1，高度2，...，*" 

- 嵌套分割

  “厂”字形嵌套

  ````html 
  <frameset rows="300,*">
      <frame src="https://baidu.com"></frame>
      <frameset cols="200,*">
           <frame src="https://lol.qq.com"></frame>
           <frame src="https://www.sina.com.cn"></frame>     
      </frameset>
  </frameset>
  ````

  ![image-20201105153156364](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201105153156364.png)

- 有时候我们想通过点击页面2的链接，内容在页面3展示，可通过如下代码实现。

  ````html
  <!doctype html>
  <HTML>
      <head>
          <title>练习主页</title>
          <meta charset="utf-8">
      </head>
  <frameset rows="200,*">
      <frame src="index.html">
      <frameset cols="200,*">
           <frame src="left.html">
           <frame src="https://www.baidu.com" name="main">
      </frameset>
  </frameset>
  </HTML>
  ````

  给页面3的框架命名。

  ````html
  <body style="color:#f00;font-size:20px">
         <a href="right.html" target="main">百度主页</a><br><br><br>
         <a href="https://https://lol.qq.com="main target="main">英雄联盟主页</a><br><br><br>
         <a href="https://https://sina.com.cn="main target="main">新浪网页</a>
  </body>
  ````

  页面2中的超链接指向框架的名字。

- 框架边框：border，令border="0"便可去掉边框。

- 子框架的设置

  \<frame src="http://www.baidu.com" name="frame" scrolling="yes|no|auto" noresize>

  语法说明： src：引入网页或文档。

  ​                     name：命名便于索引。

  ​                    scrolling：控制子窗口的滚动条。默认为auto。

  ​                     noresize：不可调整子窗口大小。

## 浮动框架（H5中仍在使用）

浏览器窗口含有孤立的子窗口，就是浮动框架，插入浮动框架要使用成对的标记\<iframe>········\</iframe>

````html
<iframe src="url" style="border:none">
    
</iframe>
````

style语句是去掉边框的语句。