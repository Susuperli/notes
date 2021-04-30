# 第四讲 文字样式

​        在HTML中我们通过文字标签\<font face="">来设置文字的字体，\<font>现在可以仍支持但是不再推荐使用。通过css的样式设置，已经能够完全的代替这个标记。

## 字体

### 字体设置

font-family:字体名称1,字体名称2,.....;

`````html
<head>
    <style>
        p{
            font-family:黑体,宋体,微软雅黑;
        }
    </style>
</head>
<body>
    <p>
        字体设置
    </p>
</body>
`````

上面字体设置会依次寻找字体，优先黑体，若不存在则是宋体，以此类推。若都不存在，则视为用户浏览器默认字体。

**注意**：在实际制作网页的时候，要尽量避免使用那些在默认的电脑系统里面没有的字体，因为大部分电脑上没有那些特殊字体，用户在显示的时候就会出现预期之外的展示效果，这并不是我们想看到的。如实在避免不了可是将其作为图片，以图片的形式上传。

### 字体大小

- 语法：font-size。

- 单位

  绝对大小（基本不用）：in（英寸）、cm（厘米）、pt（印刷点数）、pc（1pc=12pt）。

  相对大小（一般用）：px（像素）、%、em（倍数）

- **单位说明：所有浏览器字体默认大小为16px。**

  ​                     **px是基于屏幕大小和分辨率。**

  ​                    **%是基于其父元素的大小。**

  ​                     **em：是基于其父元素font-size的倍数。**

### **字体粗细**

font-weight：lighter（细体）|normal（正常）|bold（加粗）|100-900（九级粗细）

其中100=lighter，400=normal，900=bold。

### 斜体

font-style:italic（斜体）|oblique（倾斜）|normal（正常）;

斜体是一种很简单的字体风格，对字体的结构有一些小改动，来反映变化的外观。与之不同，倾斜文本则是正常版本的倾斜版本（一般不用，因为有的不支持），显示效果相同。normal大多数用来对于超链接或者地址的拉直。

## 颜色

语法：color:red;

支持英文单词，#00f，rgb(1,255,0),和rgba(0,0,255,0.5)四种设置方法。最后一种a是指不透明度可设置0~1.

## 文字的效果和线条设置

### 文字的阴影效果

语法：text-shadow:10px 5px 5px #ccc;

语法说明：**第一个参数表示阴影的水平位置；**

​                 **第二个参数表示阴影的垂直位置；（这两个必须要有）**

​                 第三个参数表示阴影的模糊距离；

​                 第四个参数表示设置阴影的颜色。

### 文字的线条设置

语法：text-decoration:underline(下划线)|overline(顶划线)|line-through(删除线)|blink(发光，没有浏览器支持)|none(没有线，一般用于去掉超链接或者地址的下划线)。

### 英文字母的大小写

英文字母大小写转换是css提供的很实用的功能之一，我们只需要设置css的属性就可以很轻松地实现英文的大小写的自动转换。

text-transform:captionlize(首字母大写)|uppercase(全部大写)|lowercase(全部小写)。

### 省略文本标记

语法：text-overflow:clip|ellipsis;

说明：clip表示修剪去文本超出部分的段落。

​            ellipsis表示用省略号代表被修剪的文本。

**注：text-overflow属性要配合overflow:hidden一起用才可以起作用。**

​         **overflow:hidden|auto；可以用于任何内容。hidden表示超出部分隐藏，auto表示超出的部分出现滚动条。**

### 水平对齐方式

text-align:left|right|center|justify;（两端对齐，大部分浏览器并不支持，所以不常用）

注：如果将此标记用于行内标记的时候（由于行内标记的宽高是指本身内容的宽高，无法对其进行设置，无论居左、右或是中都无法起作用），可以在此行内标记外面套一个块级标记，然后对块级标记使用水平居中标记，功能便可实现。如果是对于块级套块级标记，还需要对次级块级使用如下代码margin:0 auto;

`````html
		<style>
			.one{
				text-align:center;
				border:1px black solid;
			}
			.two{
				border:1px red solid;
				width:50%;
				margin:0 auto;
			}
		</style>



		<div class="one">
			<div class="two">
				我的世界
			</div>
		</div>
`````

显示效果：这里需要注意的是，对于"%"来说也是分中英文的，注意区分（中文的大一些）。![image-20201112152257103](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201112152257103.png)

### 垂直对齐方式

语法：vertical-align:top|middle|bottom;

段落的垂直居中仅是可以作用于表格。一般来说对于其他的块级标记来说并不可用，但是可以通过display:table-cell;语句把主级转换成一个单元格，借此来“欺骗”浏览器，来满足表格的条件，来进行垂直居中。

### 强制文本换行

语法：word-wrap:normal|break-word;

在网页中长单词一般是不会自动换行的，通过此语句可以使单词强制换行。默认是normal。

### 行间距

**语法：line-height:npx;**

说明：他表示的是两横文字之间基线的距离，如果给文字加上下划线，那么下划线的位置就称为基线。其单位可以是相对值也可以是绝对值。在只有一行文字时，也可以做水平居中,将line-height的高度设置成与该块级标记高度一样，便可以实现垂直居中，一般用在按钮身上。

````html
<style>
    div{
	    width:200px;
	    height:100px;
	    text-align:center;
	    border:1px black solid;
           line-height:100px;
	}
</style>
````

### 字间距

语法：letter-spacing

说明：设置字母与字母之间的距离，他的值可以是绝对值也可以是相对值。

### css自定义字体

语法：@font-face{

​                              font-family:name;

​                              src:url("路径");

​                               font-weight:normal|bold;

​           }

说明：可以自定义字体（常用），name为自己自定义的名字。src可以接字体库的路径。可以解决一部分特殊字体用户浏览器中没有的困扰。大部分是自己建一个字体库，里面用上一些小的简笔画、矢量图之类的（可以在阿里矢量图库中搜寻），完成引入，减少网页打开时间。

## 补充内容 

- box-shadow：设置盒子（元素）阴影，用法同文字阴影效果。
- 对于超链接\<a>和表单输入\<input>的字体样式需要单独设置，不能继承其父元素样式。

### 浅析块级元素的水平居中margin:0 auto;

参考博客[margin到底相对谁？_xiaowei的博客-CSDN博客](https://blog.csdn.net/u013217071/article/details/52489281)

- margin到底相对于谁

  - 外边距合并现象

    如果两个div上下排列，给上面div设置margin-bottom，给下面div设置margin-top，那么两个margin会发生合并现象，会取较大的margin值。

    注意：左右不会发生 外边距合并现象

  - 上下塌陷现象

    **一个大盒子 中包含一个小盒子，给小盒子设置一个margin-top，大盒子会一起向下平移。**

    注意：margin左右没有塌陷现象

  如果父元素在子元素的margin的同向上有padding或border的话，子元素的margin相对于父元素，否则相对于父元素以外的元素。**且为大盒子增加边框或是padding-top会变正常。**

- 为何会居中

  参考博客：[margin:0 auto为何会居中? - 残梦a - 博客园 (cnblogs.com)](https://www.cnblogs.com/sunhang32/p/11826580.html)

  - 首先如果想要**设置居中,width是必须设置的**,如果不设置width元素,那么块级元素一定会占据100%的宽度,margin:0 auto的auto是指平分剩余空间,比如宽度为200,父元素的宽度为1000,那么auto就是指水平方向平分剩余的宽度(1000-200/2)。













