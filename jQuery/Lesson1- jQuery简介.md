# 第一讲 jQuery简介

## js框架

为了简化JavaScript的开发，JavaScript框架就诞生了。

比较流行的JavaScript框架

- prototype
- Dojo
- YUI
- Angular.js
- Zepto.js
- jQuery

## jQuery优势

​      **轻量级，强大的选择器，出色的DOM封装，可靠的事件处理机制，完善的Ajax，不污染的顶级变量，出色的浏览器兼容性，链式操作方式，隐式迭代，丰富的插件，完善的文档，开源。**

## jQuery代码风格

 ### 引入库文件

````html
<script src="jquery-1.8.3.min.js" type="text/javascript"></script>
````

**注**：自己编写的jQuery的代码也要写在库里面。

### 书写

````js
$(document).ready(function(){
    alert($("h3").html());
})
````

其中

- $()代表了jQuery的对象，是jQuery的简写形式。
- $(document).ready表示在html文档加载完成后执行的函数简写形式。
- $("h3").html()获取文档的标注内容，$("h3")，相当于js中的document.getElementsByTagName("h3")。