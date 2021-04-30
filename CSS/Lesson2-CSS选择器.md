# 第二讲 CSS选择器

## css选择器

选择器是css中很重要的概念，所有HTML中都是通过不同的css选择进行控制的，给选择赋予各种样式声明，即可实现各种效果。

类比有基本选择器、层次关系选择器、伪类选择器。

## 基本选择器

### 标记选择器

和标记名称相同的选择器；自动应用到相同的标志中。

基本写法：p{

​                         color:#f00;

​                          font-famiy:宋体；

​                      }

### 类别选择器

类别选择器名称需要用户定义且需要手动应用到不同标记之中。

写法

````html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style>
			p{
			    color:#f00;
			    font-size:20px
			}
			.one{
				color:#0f0;
			}
			.two{
				border:1px solid #000;
			}
			.kk{
				color:#00f;
		</style>
	</head>
	<body>
		<p>这是段落</p>
		<h1 class="one two kk">这是大标题</h1>
		<h2 class="two">这是二标题</h2>
		<h3 id="first">这是三标题</h3>
		<p class="two">这是又一段</p>
		<div class="a">
			<p class="b">内容1</p>
			<p>内容2<span class="c">hello</span></p>
			<ul>
				<li><span>11</span></li>
			</ul>  
			<span>12</span>
		</div>
		<span class="d">21</span>
	</body>
</html>

````

.+命名{规则}，规则中的属性之间用;隔开遵守css的书写法则，最后一个属性值可以加可以不加。后面用class索引，匹配样式。如果要应用多个样式，可以在class中直接写出之间用空格隔开。

### ID选择器

ID选择器名称需要用户定义且需要手动应用到不同标记之中，**一个ID选择器只能在HTML中使用一次**。

使用时在\<style>中用#ID{规则}。

````html
		<style>
			#first{
				background-color:#0ff
		</style>
````

索引规则如下所示，可以在任何标记中使用，但是只能使用一次。

````html
		<h3 id="first">这是三标题</h3>          
````

### 优先级问题

ID选择器>类别选择器>标记选择器。实际上所遵守的规则是就是谁的适用范围更小谁优先显示。

1. ！important

　　　　在属性后面写上这条样式，会覆盖掉页面上任何位置定义的元素的样式。

　　2.  行内样式，在style属性里面写的样式。

　　3. id选择器

　　4. class选择器

　　5. 标签选择器

6. 通配符选择器

　　7. 浏览器的自定义属性和继承

#### 优先级的权重问题

　 **!important                Infinity[正无穷]**

​     **行间选择器               1000[权重]**

​     **id选择器                 100[权重]**

​     **class|属性|伪类选择器     10[权重]**

​    **标签|伪元素选择器         1\[权重]**

​    **通配符                    0[权重]**

## 层次关系选择器

- selector1 selector2。包含选择器，选择包括1里面的所用的结构或是段落。

  ````html
  <style>
     	div span{
  	     color:red;
  		}
  </style>
  ````

  表示属于所有div中所有的span中的元素。

- selector1，selector2，selector3。选择匹配，1,2，3若有相同属性和属性值都可以打包起来放在这一个地方。**（举例？）**

- selector1>selector2。子元素选择器，选择1里面所有的子元素。

  ````html
  <style>
     	div>span{
  	     color:red;
  		}
  </style>
  ````

  只包括子元素。

- selector1+selector2。选择下一个紧挨着的兄弟元素。

  ````html
  <style>
     	div+span{
  	     color:red;
  			}
  </style>
  ````

## 全局声明

全局声明*，初始化样式。

````html
<style>
    *{
        color:#f00;
    }
</style>
````

作用于全局。

## css继承

- 父子关系：在大多数的文字样式中，给父元素的文字样式其子元素大多是可以继承的（颜色啥的可以，border则不能），并且可以在父元素的基础上再加以修改。子元素的风格不会影响父元素。

