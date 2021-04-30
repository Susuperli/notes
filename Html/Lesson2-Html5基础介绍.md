# 第二课 Html5基础介绍

## 概念及HTML5新增功能

### 概念及优势

- html是指Hypertext Marup Lauguage的英文简称，即超文本标记语语言。
- html5具有如下优势：化繁为简、向下兼容、语义化标签、实用性、用户优先、通用访问。

### 新增功能

- **canvas绘图**（新增特色功能，可以用来做游戏）
- **跨文本消息传递**（简化数据传输）
- 地理位置（定位）
- 本地存储（将网上加载过的内容保存到本地，加快加载速度）
- 本地数据库

## 基本语法

### 标记语法

- **单标记**

  是指单独使用就可以表达完整的意思，其基本语法为：<标记名称>。

  例如:\<br>,\<img>,\<input>.

- **双标记**

  是指由首标记和尾标记两部分构成，它必须成对使用。其基本语法为：<标记名称> 内容</标记名称>。

  其中内容是指被这两个标记施加作用的部分，可以嵌套但是不能交叉使用。

  例如:\<html>    内容 \</html>  ,\<head>  内容  \</head>。

- 属性语法

  HTML通过标记告诉浏览如何展示网页，另外还可以为某些元素附加一些信息，这些信息称为属性。

  其基本语法为：<标记名称 属性名1="属性值1" 属性名2="属性值2".....>

  例如:插入一条宽为5px的，居中的直线，所使用的代码如下。

  ```html
  <hr size="5" align="center">
  ```

- 注释

  在源代码中插入注释，浏览器工作时会将其忽略，可以使用注释的方法对源代码进行解释，便于理解和后期修改。

  基本语法：\<!--注释内容-->

## 基本结构

基本结构如下表示

```html
<!doctype html>
<html>
    <head> 
        <title>网页标题</title>
        <meta charset="utf-8">
    </head>
    
    <body>
        hello world
    </body>  
</html>
```

### DOCTYPE声名

​        大多数页面的开头通常是**使用doctype来标记声明用使用的什么风格的HTML或者XHTML，doctype使浏览器知道应该如何处理文档，并且让浏览器知道按照什么标准检查代码的语法。**如果没有标记则浏览器默认最等低规则检查，新的标记无法识别导致错误。

​         **所举列子为HTML5最新的**，也是使用最多的生声明方法（记住）

```html
<!doctype html>
```

   **其他版本doctype声明方法举例**（不要求记忆，但是见到了要认识）

- HTML4.01文档过渡定义类型，此类型定义的文档可以使用HTML中的标签与元素包括一些不被W3C推荐的标签（例如：font、b等），不可以使用框架。

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
  ```

- HTML4.01文档严格定义类型，此类型定义的文档可以使用HTML中的标签与元素，不能包含不被W3C推荐的标签（例如：font、b等），不可以使用框架。

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dt
  ```

- HTML4.01文档框架定义类型，此类型等同于HTML4.01文档过渡定义类型，但可以使用框架。

  ```html
  <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
  ```

- XHTML1.0文档过渡定义类型，此类型定义的文档可以使用HTML中的标签与元素包括一些不被W3C推荐的标签（例如：font、b等），不可以使用框架。

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
  ```

- XHTML1.0文档严格定义类型，此类型定义的文档只可以使用HTML中定义的标签与元素，不能包含不被W3C推荐的标签（例如：font、b），不可以使用框架。

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
  ```

- XHTML1.0文档框架定义类型，等同于XHTML1.0文档过渡定义类型，但可以使用框架。

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
  ```

- XHTML1.1文档严格定义类型，等同于XHTML1.0文档过渡定义类型。

  ```html
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
  ```

- HTML5文档类型。

  ```html
  <!DOCTYPE html>
  ```

### 头部内容

头部内容，即\<head>\</head>之间的内容是不被显示在正文中，允许写入头部标记中的**仅有**如下

|       \<meta>       |   设置原信息   |
| :-----------------: | :------------: |
|  \<title>\</title>  |    网页标题    |
|  \<style>\</style>  |    引入css     |
|       \<link>       |  引入css文件   |
| \<script>\</script> | 引入javascript |

- 通过name设置网页的制作工具（不常用）

  ```html
  <meta name="generator" content="相应开发工具（例如txt）">
  ```

- **Keywords设置网页keywords，便于搜索引擎搜索**（常用）

  SEO---搜索引擎优化

  ```html
  <meta name="keywords" content="关键字">
  ```

- **Discription设置网页描述**（作用和keywords差不多，都用于搜索）

  ```html
  <meta name="discription" content="相应描述">
  ```

- Author 声明作者（可以不写）

  ```html
  <meta name="author" content="作者名字">
  ```

- **Content-Type声明网页采用的字符集**（必写）

  ```html
  <meta http-equiv="content-type" content="text/html;charset=utf-8">
  ```

  ```html
  <meta charset="utf-8">   (这是h5简化后的写法)
  ```

  >常见问题：有时使用文本文档设置utf-8后，在浏览器打开反而乱码。
  >
  >原因：文本文档的内置字符集和浏览器的字符集冲突。
  >
  >解决方案：在文本文档保存时将编码方式选为utf-8

- **设置浏览器内核版本，提高兼容性**

  ```html
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/>       <!--compatible为兼容的意思-->
  ```

**注**：这个后面加了一个“/”，这是xtml的语法，其实也可以不加。

## 注意事项

- “<”和“>”是任何标记的开始和结束，双标记必须关闭。
- 标记可以嵌套但是不可以交叉
- **标记中可以放置各种属性，属性值用""括起来**。
- 标签名和属性名建议小写
- 使用缩进风格便于理解代码
- 文件保存时扩展名为.html或者.htm，建议统一使用.html。
- 文件名只可以由英文字母，数字，下划线组成；文件名区分大小写。
- **网站首页文件名一般是index/html**。

## 补充内容

**XHTML**
可扩展超文本标记语言，基于可扩展标记语言（XML）的标记语言
         2000年底，国际W3C组织（万维网联盟）组织公布发行了XHTML 1.0版本。XHTML 1.0是一种在HTML 4.0基础上优化和改进的的新语言，目的是基于XML应用。XHTML是一种增强了的HTML,XHTML 是更严谨更纯净的 HTML 版本。

​         HTML是当前HTML版的继承者。HTML语法要求比较松散，这样对网页编写者来说，比较方便，但对于机器来说，语言的语法越松散，处理起来就越困难，对于传统的计算机来说，还有能力兼容松散语法，但对于许多其他设备，比如手机，难度就比较大。因此产生了由DTD定义规则，语法要求更加严格的XHTML。

语法规则
        所有标签必须闭合，也就是说开始标签要有相应的结束标签。、XHTML中所有的标签必须小写。在XHTML中，所有的参数值，包括数字，必须用双引号括起来。
所有元素，包括空元素，比如img、br等，也都必须闭合，实现的方式是在开始标签末尾加入斜扛，比如<img … /> 、\<br />。省略参数，比如\<option selected>，也不允许，必须用\<option selected="selected"/>。

**XML**
可扩展标记语言
       1998年2月，W3C正式批准了可扩展标记语言的标准定义，可扩展标记语言可以对文档和数据进行结构化处理，从而能够在部门、客户和供应商之间进行交换，实现动态内容生成，企业集成和应用开发。可扩展标记语言可以使我们能够更准确的搜索，更方便的传送软件组件，更好的描述一些事物。例如电子商务交易等。
它被设计用来传输和存储数据；
超文本标记语言被设计用来显示数据。
它们都是标准通用标记语言的子集。

**一、什么是可扩展标记语言？**
可扩展标记语言是一种很像超文本标记语言的标记语言。
它的设计宗旨是传输数据，而不是显示数据。
它的标签没有被预定义。您需要自行定义标签。
它被设计为具有自我描述性。
它是W3C的推荐标准。

**二、可扩展标记语言和超文本标记语言之间的差异**
它不是超文本标记语言的替代。
它是对超文本标记语言的补充。
它和超文本标记语言为不同的目的而设计：
它被设计用来传输和存储数据，其焦点是数据的内容。
超文本标记语言被设计用来显示数据，其焦点是数据的外观。

**HTML**
超文本标记语言

**HTML5**
万维网的核心语言、标准通用标记语言下的一个应用超文本标记语言 （HTML）的第五次重大修改
2014年10月29日，万维网联盟宣布，经过接近8年的艰苦努力，该标准规范终于制定完成。

