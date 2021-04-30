# 第十四讲 CSS中补充内容1——兼容性和优先级

## 水平居中的方法

### 定位拉回

`````html
<style>
    .parent{
        width:200px;
        height:200px;
        background-color:red;
    }
    .child{
        width:100px;
        height:100px;
        background-color:black;
        position:absolute;
        top:50%;
        margin-top:-50px;
        left:50%;
        margin-left:-50px;
    }
</style>
`````

### 定位margin

````html

````

### table-cell

### line-height

## 兼容性问题的解决

### 兼容性产生的原因

由于不同厂商的浏览器或某一个浏览器的不同版本对于css的支持和解析不一样，导致在不同浏览器的环境中呈现出不一致的页面展示的效果。

### 主流浏览器内核

- trident内核：主要在IE浏览器中使用。
- gecko内核：是Firefox浏览器的内核。
- webkit内核：主要是Chrome和Safari的内核，以及最新版本的edge浏览器。
- presto内核：是低版本的Opera浏览器的内核，最新本的Opera浏览器使用blink内核。

### 解决兼容性方法

- css reset

  通过重置css默认样式解决最基本的兼容性问题。最简单的就是设置全局申明。

- css hack

  - 什么是css hack？

    由于不同厂商的浏览器或某一个浏览器的不同版本对于css的支持和解析不一样，导致在不同浏览器的环境中呈现出不一致的页面展示的效果。这时，我们为了或得统一的页面效果，就需要针对不同的浏览器或是相同浏览器的不同版本写特定的样式，**我们把这个针对不同浏览器不同版本的写相应的css code的过程叫做css hack。**

  - css hack分类

    大只有三种表现方法：**css属性前缀法**、**选择器前缀法**（几乎是不用）、**IE浏览器的条件注释法**（即HTML头部引入if IE）实际项目中css hack大部分是针对IE浏览器不同版本之间的表现差异而引入的。

  - 常见的css前缀

    -moz-：Firefox

    -ms-：IE

    -webkit-：Chrome

    -o-：Opera

  - 条件注释法

    这种方法是IE浏览器独有的hack方式，微软官方推荐使用的hack方式（IE9及其以下版本不支持）。

    **只在ie下生效**

    \<!--[if IE]>这段话只在IE浏览器中显示<![endif]-->

    **只在ie6生效**

    \<!--[if IE6]>这段话只在IE6浏览器中显示<![endif]-->

    **只在ie6以上生效**

    \<!--[if gte IE6]>这段话只在IE6浏览器中显示<![endif]-->

    **只有ie8不生效**

    \<!--[if ! IE8]>这段话只在IE6浏览器中显示<![endif]-->

- 针对IE6的方法

## 其他常见问题

### 图片下方间距间隙问题

产生的时机：图像下方添加块状元素，之间会产生间隙，在Firefox、IE、Chrome中都存在此问题。

解决方法：给图片标记添加display:block;，或者设置vertical-align，实际中浮动也可以解决。

### 解决低版本IE不支持新增html5标记

在文档中引入HTML5shiv.js插件

### css中优先级问题

- 行内大于其他，其他中遵循就近原则。
- ID>类别>标记。越具体优先级就越高。
- 其他优先级比较
  -  !important标记的优先级是最高的。
  - 优先级相同时，就近原则。
  - **继承来的属性，优先级最低**。



