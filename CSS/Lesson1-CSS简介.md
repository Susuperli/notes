# 第一讲 CSS简介

## 简介

### 概念

层叠样式表，它适用于控制网页样式并允许样式信息与网页内容分离的一种标记性语言。

### HTML缺点

- 维护困难
- 标记不足
- 代码冗余
- 定位困难

## 如何使用css控制页面

css可以使用在任何HTML的标记中，使用方法分为四类分别为，行内标记、内嵌式标记、链接式标记和导入式标记。

- **行内式标记**（优先级最高）

  将css代码直接写在标记中和HTML属性的使用方法一样。（属性值要带单位展示）

  ````html
  <p style="color:#0f0;font-size:20px">
      正文
  </p>
  ````

    每个标记都设置了style，后期维护依然成本高，而且网页容易过胖，因此不推荐使用，不同原属性之间用;隔开。

- 嵌入式标记

  ````html
  <head>
      <title>嘿嘿</title>
      <meta charset="utf-8">
      <style type="text/css">
          p{color:#f00;
            font-family:黑体
           }
      </style>
  </head>
  <body>
      <p>
          正文
      </p>
      <p>
          zjj 
      </p>
  </body>
  ````

  方便后期维护，代码本身瘦身，但是一个网站会拥有多各个页面，内嵌就很麻烦了，仅适用于特殊页面设置。

- **链接式标记（使用最多**）

  使用频率最高，也是最实用的方法，将HTML代码与css样式的分离为两个或者多个文件，实现了页面框架HTML和美工代码css的完全分离，是前期制作和后勤维护都十分方便。而且对于同一个css文件可以链接到多个HTML文件中，甚至可以链接到整个网络的所有页面中，使网页风格统一。

  ````html
  <head>
      <link href="ioashdoia.css" type="text/css" rel="stylesheet">
  </head>
  ````

- 导入式标记

  导入式和链接式功能基本相同，在\<style>\</style>中使用@import导入样式。

  @import url("1.css")

  @import "1.css"

  **链接式和导入式两种都是外部引用css方式，但是还有一定的区别**

  - link是HTML标签，除了加载css之外，还可以定义rss等其他事务；@import属于css范围，只能加载css。
  - **link引用css时在本页面载入时同时加载；@import需要页面完全载入以后才可以加载（主要原因）。**
  - link是XHTML标记没有兼容性问题；@import是css2.1提出的，低版本的浏览器你不可以运行。
  - link支持使用JavaScript控制样式，而@import不支持。

