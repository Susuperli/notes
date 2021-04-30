# 第六讲 使用css控制列表样式

## 列表的符号

- 语法：list-style-type:属性值；

- 属性值：disc、circle、square、decimal（1,2,3）图片的符号，upper-alpha(大写字母)、lower-alpha(小写字母)、upper-Roman(大写罗马数字)、lower-roman(小写罗马数字)、none(用的最多的)。

- 举例

  `````html
  <style>
      list-style-type:decimal;
  </style>
  `````

## 图片符号

- 语法：list-style-image:url("icon,ipg")

- 说明：不同的浏览器对于此语句的显示效果不同，不建议使用。

  通常先将：ul{

  ​                     list-style-type:none;

  ​                 }

  完事是将background将：li{

  ​                                          background-image:url("路径")

  ​                                        }

- 举例

  ````html
  		<style>
  			ul{
				       margin:0;
  				padding:0px;
				       /*font-size:50px;*/
  				list-style-type:none;/*去除列表自身的格式*/
  				height:30px;/*设置宽高*/
  				width:400px;
  				margin:0 auto;/*使列表居中*/
  			}
  			li{
  				background-image:url(kkk.png);/*设置路径*/
  				background-repeat:no-repeat;/*不让图片重复*/
  				background-position:left-center;/*更改位置*/
  				padding-left:20px;/*与图片拉开距离*/
  				background-size:20px 20px;/*设置图片大小，以适应列表*/
  			}
  		</style>
  ````
  

## 制作无序列表的菜单

- 由于\<a>在一些浏览器中不支持width和height所以需要将\<a>标记设置为块级元素，display:block;，设置为块级元素后\<a>标记就会自动填充满\<li>的区域，鼠标滑入该处的任何部分时就可以点击到。

- 举例

  ````html
  <!DOCTYPE html>
  <html>
	<head>
  		<meta charset="utf-8">
  		<title>无序列表菜单</title>
  			<style type="text/css">
  				ul{
  					list-style-type:none;
  					margin:0;
  					padding:0;
  				}/*取消列表原有的各种样式，便于后面统一更改*/
  				a{
  					text-decoration:none;
  					display:block;
  					color:black;
  					background-color: antiquewhite;
  				}/*设置超链接的属性，注意这里要将超链接设置成块级标记，方便控制宽高以及里面的背景颜色*/
  				.nav{
  					background-color:red;/*此语句并不产生效果*/
  					width:800px;
  					text-align:center;
  					color:white;
  				}/*设置nav的样式，浮动后里面的背景颜色不能被继承，这里的背景颜色不用设置，主要是宽度的设置要合理*/
  				a:hover{
  					background-color:cyan;
  				}/*鼠标指向超链接子列表的背景颜色*/
  				.nav>li{
  					float:left;
  					width:199px;
  					border-right:1px solid black;
  					background-color:yellow;
  				}/*浮动以横向排列，子列表的样式，这里要注意的是宽度和border宽度*/
  				.nav li ul{
  					display:none;
  				}/*将子列表藏起来*/
  				.nav>li:hover>ul{
  					display:block;
  				}/*本次的核心语句，当鼠标滑入父列表时，显示子列表*/
  			</style>
  	</head>
  	<body>
  		<ul class="nav">
  			<li>电脑
  			    <ul>
  				    <li><a href="#">惠普</a></li>
  				    <li><a href="#">华硕</a></li>
  				    <li><a href="#">联想</a></li>
  			    </ul>
  			</li>
  			<li>冰箱
  			    <ul>
  			        <li><a href="#">海尔</a></li>
  				    <li><a href="#">美的</a></li>
  					<li><a href="#">西门子</a></li>
  			    </ul>
  			</li>
  		    <li>手机
  			    <ul>
  			    	<li><a href="#">华为</a></li>
  					<li><a href="#">小米</a></li>
  					<li><a href="#">苹果</a></li>
  					<li><a href="#">三星</a></li>
  			    </ul>
  		     </li>
  			 <li>电视机
  			     <ul>
  			     	<li><a href="#">索尼</a></li>
  					<li><a href="#">海信</a></li>
  					<li><a href="#">康佳</a></li>
  			     </ul>
  			 </li>
  		</ul>
  	</body>
  </html>
  ````
  
  ![image-20201114233006746](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201114233006746.png)

## 补充

display:none;隐藏，位置和内容都会隐藏。

**Visibility**:hidden|visible;内容会隐藏，但是位置还在，视觉效果。

