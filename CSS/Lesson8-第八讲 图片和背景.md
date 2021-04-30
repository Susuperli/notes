# 第八讲 图片和背景

## 图片样式

### 图片边框

border-style：定义边框的样式。

border-color：定义边框颜色。

border-width：定义边框粗细。

### 图片的对齐

- 横向，对其父元素使用text-align:left|center|right，让他继承这些属性。
- 纵向，将父元素设置成单元格模式，再使用verticle-align

## 背景图片

### 设置背景颜色

background-color:#ff0000;

支持各种方式的颜色声明：包括十六进制、rgb模式、英文单词模式、rgba模式。

**同样支持透明度的样式语句还有opacity:0.5;跟rgba不同的是，它设置的是整个标记的透明度；而rgba只是表示背景颜色透明度注意甄别。**

**遮罩层举例**

````html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			.one{
				width:300px;
				height:200px;
				position:relative;
			}
			img{
				width:300px;
				height:200px;
				position:absolute;
				top:0;
				left:0;
				/*display:block;
				margin:0 auto;*//*这段语句可以去掉3pxbug*/
			}
			.two{
				width:300px;
				height:200px;
				background-color:rgba(0,0,0,0.5);
				position:absolute;
				top:0;
				left:0;
				display:none;
			}
			.one:hover>.two{
				display: block;
			}
		</style>
	</head>
	<body>
		<div class="one">
			<img src="css8.png" >
                    <div class="two">
		      </div>
		</div>
	</body>
</html>
````

### 渐变背景色

#### 水平渐变

- 语法：background-image:linear-gradient(方向,颜色1,颜色2,颜色3,.....);

- 设置线性渐变，方向参数to top|bottom|left|right，还可以是对角的形式比如，to left top|right top，除了上下左右这种方式，还可以设置具体的角度比如，0deg，45deg，90deg制定具体的角度。

#### 径向渐变

- 语法：background-image:radial-gradient(颜色1,颜色2,...);

- 径向是没有方向一说，本身就是由内指向外面的渐变。

### 背景图片

#### 插入背景图片

语法：background-image:url(路径);来引入背景图片。

#### 背景图片的重复

语法：background-repeat:repeat(默认)|repeat-x(水平方向的重复)|repeat-y(垂直方向的重复)|no-repeat(不重复);。

#### 背景图片的位置

语法：background-position:top left|top center|top right|center left;等等组合。也可以是具体坐标background-position:20px 20px;坐标的计算规则是，以标记的左上角为原点，左为x正，下为y正。也可以是百分比background-position:20%,20%;。

#### 背景图片的固定

语法：background-attachment:fixed;固定背景图片，这里的固定是相对于浏览器来说，例如固定在左上角在浏览时就会一直在浏览器的固定位置显示。

#### 背景图片的大小

语法：background-size:100%,100%;

#### 背景颜色的综合设置

- background-color:#ff0000;颜色。

- background-image:url();图片路径。

- backgrond-repeat:no-repeat;重复。

- backgrond-attachment:fixed;固定。
- background-position:10px,20px;位置。

- background-size:100%,100%;大小。

- 综合设置：

  background:#f00 url() no-repeat fixed 5px 10px;

  background-size:100%,100%;

  大小不可用跟他们写一块，大概是怕跟位置混了。

#### **设置多个背景颜色时**

background-color:#ff0,#000;

background-image:url(),url();

backgrond-repeat:no-repeat;

backgrond-attachment:fixed

background-position:10px 20px,20px 30px;

background-size:100%,100%;

从后面直接写出即可，不能从后面再写一个会覆盖。