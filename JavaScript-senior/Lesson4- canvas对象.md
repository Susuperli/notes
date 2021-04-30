# 第四讲  canvas对象

## 渲染上下文

canvas起初是空白的，想要绘制图像，首先需要使用脚本渲染上下文，然后在它的上面绘制，getContext()方式，用来或得渲染上下文和它的绘画功能，该方法唯一一个合法参数'2d'（将来可能会支持3d)使用该方法也可以检测浏览器是否支持浏览器支持canvas对象。

````js
var mycanvas=document.getElementById("mycanvas")
var ctx=mycanvas.getContext('2d')
````

## 绘制矩形

- fillRect(x,y,width,heght):绘制一个可填充的矩形。
- strokeRect(x,y,width,height):绘制一个矩形边框。
- clearRect(x,y,width,height):清除指定的矩形区域，然后这块区域会变的完全透明。

## 绘制路径

### 步骤如下

- 创建路径起点
- 调用绘制方法去绘制路径
- 把路径封闭
- 一旦路径生成，通过描边或填充路径区域来渲染图形

### 方法如下

- beginPath()；开始新路径
- moveTo(x,y);起点
- lineTo(x,y)；画一条直线到
- closePath(x,y);关闭路径
- stroke()；通过线条来绘制图形轮廓
- fill()；通过填充路径的内容区域生成实心的图像

## 绘制圆弧

````js
arc(x,y,r,startAngle,endAngle,anticlockwise)  
````

x,y为圆心；r为半径；startAngle,endAngle其中角度的表示方法为弧度制；anticlockwise的值为布尔型，默认false为顺时针。

````js
	var canvas=document.getElementById("canvas");
	function change(){
		if(canvas.getContext){  //判断是否支持canvas对象
			var ctx=canvas.getContext('2d');
			ctx.beginPath();
			// ctx.moveTo(100,100);
			// ctx.lineTo(100,200);
			// ctx.lineTo(200,200);
			// ctx.lineTo(200,100);
			var color1=[0,1,2,3,4,5,6,7,8,9,'a','b','c','d','e','f']
			var str="";
			for(var i=0;i<3;i++){
				str+=color1[(Math.floor(Math.random()*16))]
			}
			ctx.arc(Math.random()*501,Math.random()*501,Math.random()*100,0,2*Math.PI,false)
			ctx.closePath();
			ctx.fillStyle="#"+str;
			ctx.strokeStyle="ff0"
			ctx.fill()
		}
	}
	change();
	setInterval(change,300)
````

## 绘制贝塞尔曲线

![mark](http://qiniu.cloud-zhi.com/blog/210430/eeH44DeDif.png?imageslim)

## 绘制文本

### 线段末端样式

ctx.lineCap=type; 

- butt：线段末端以方形结束。
- round：线段末端以圆形结束。
- square：线段末端以方形结束，但是增加了一个宽度和线段相同，高度是线段厚度一半的矩形区域。![mark](http://qiniu.cloud-zhi.com/blog/210430/Df6mD8eej3.png?imageslim)

![mark](http://qiniu.cloud-zhi.com/blog/210430/Fc9F7gf1A9.png?imageslim)

![mark](http://qiniu.cloud-zhi.com/blog/210430/hG7cL58EiI.png?imageslim)

## 绘制图片

使用drawImage()方法。

`````js
drawImage(image,x,y) //写入canvas，image表示图片对象。x,y是图片原点的位置（左上角）
drawImage(image,x,y,height)//写入图片同时进行缩放
`````

图像切片

````js
drawImage(image,sx,sy,swidth,sheight,dx,dy,dwidth,dheight);
````

- sx和sy表示截取图像位置的起点，也就是左上角点。
- swidth和sheight表示要截取的宽高。
- dx和dy表示截取后图片在canvas当中的左上角位置。
- dwidth和dheight表示写入的图片的大小。

放大镜

`````html
<!DOCTYPE html>
<html lang="zh">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title></title>
</head>

<body>
	<img src="../picture/img-f520797d57c7fac6334a6cb9a8ca9126.jpg" id="imga" style="width: 600px; height: auto;">
	<canvas id="canvas" width="300" height="300" style="border: black solid 1px;"></canvas>
</body>
<script type="text/javascript">
	var img = document.getElementById("imga");
	var canvas = document.getElementById("canvas");
	if (canvas.getContext) {
		var ctx = canvas.getContext('2d');
		img.onload = function () {
			img.onmousemove=function(e){
				var x=e.offsetX*1.78-150;
				var y=e.offsetY*1.78-150;
				console.log(x)
				ctx.clearRect(0,0,300,300)
				ctx.drawImage(img, x, y, 300, 300, 0, 0, 300, 300)
			}
		}
	}
</script>
</html>
`````

