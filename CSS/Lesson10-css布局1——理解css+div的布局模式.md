# 第十讲 css布局1——理解css+div的布局模式

## 简介

说明：网页中各种元素都必须有自己合理的位置，从而搭建出整个页面的结构。主要是通过下面的标记：float、position、z-index。

## 浮动float

### 浮动

float定位是css排版中非常重要的手段，当设置元素向左或是向右浮动时，元素也会向左或是向右紧靠。主要是通过如下语句float:left|right|none(默认);。

### 兄弟结构中

在body中写入如下代码，1和2构成兄弟元素。具有如下特点：

````html
	<body>
		<div class="one">1</div>
		<div class="two">2</div>
	</body>

<style>
   	.one{
		background-color:red;
		float:left;
	}
	.two{
		background-color: #0000FF;
		/*float:left;*/
	}
</style>

````

- 只给上面的元素设置浮动时，这个div的宽度会变成内容的宽度，并且会根据左右浮动向左或是向右靠边。并且会使其脱离文档流。后面的元素会占据其位置。**对前面的元素并无影响。**

  ![image-20201122112505034](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201122112505034.png)

- 如果两个相邻块级的元素都给设置浮动，那么他们就会水平排列。

  ![image-20201122112946768](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201122112946768.png)

### 父子结构中

在如下的父子结构中

````html
	<body>
		<div class="one">
			<div class="two">你好啊</div>
		</div>
		<!-- <div class="three">你好吗</div> -->
	</body>



<style>
      	.one{
		background-color:red;
		border: #000000 1px solid;
		/*float:left;*/
	}
	.two{
		background-color: #0000FF;
		float:left;
	}
</style>


````

- 当子元素使用浮动时，且父元素中并无其他元素，这时由于子元素脱离文档流而导致无法支撑父元素，就会造成父元素的“塌陷”。

  ![image-20201122113649028](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201122113649028.png)

- 当父元素浮动时，父元素会带着子元素一块脱离文档流，但是父子关系依旧存在。

  ![image-20201122113923935](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201122113923935.png)

- 父子都会脱离文档流，同上。

### 消除浮动

- 清除前面因设置浮动的元素的对之后元素造成的影响。

  clear:left|right|both；分别对应消除对于左、右、两边的浮动。

- 解决因子元素浮动而造成父元素塌陷的影响

  - 设置父元素的高度。
  - 给父元素添加overflow:hidden;。

## 定位position

### 定位

- position用来指定块元素相对于父级块元素的位置和相对于他自己本身的位置。
- position一共有四个值，分别是static（默认）、absolute、relative和fixed，默认表示该元素保持在原位置不动。
- position定位要配和top、right、bottom、left这四个属性进行定位，属性值可以是具体像素也可以是百分数。

### 绝对定位

当子元素的position属性值设置为absolute时，**子块也变不再是属于父级**。

- 兄弟结构中

  - 当一个元素设置了绝对定位时，他的宽高也就变成了内容的宽高，本身脱离文档流。

    **当在position下面设置得位置top和left时，绝对定位就会相对于元素左上角做定位；当设置是bottom和right时相对于右下角做定位，以此类推。**

    ````html
    <style>
        	.one{
    		background-color:red;
    		position:absolute;
    		top: 20px;
    		left: 20px;
    			}
    </style>
    
    
    
    	<body>
    		<div class="one">你好啊</div>
    		<div class="two">你好啊</div>
    		<!-- <div class="three">你好吗</div> -->
    	</body>
    ````

    ![image-20201122134424727](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201122134424727.png)

  - 当前面元素使用position时，后面的元素会占据前面的位置，但是前面的元素会显示在上方；如果有多个元素使用position定位在一点时，最后面的元素会显示在最上层。后面使用position对前面的元素没有影响。

- 父子结构中

  - **子元素设置position时，子元素便不在属于父元素，会在父元素下显示。当父元素中没有元素时，因为子元素的脱离，导致其塌陷；当父元素中存在内容时会正常显示内容，脱离的子元素在其下面展示。**

  - 父元素设置position时，子元素会随之脱离文档流。**？**

    ![image-20201122142725115](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201122142725115.png)

  - 父元素和子元素一块使用position时，各自脱离各自的文档流。

    ![image-20201122142746000](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201122142746000.png)

- 绝对定位都是相对于谁定位

  绝对定位是相对于离他最近的设置了定位的祖先元素定位，如果没有则是相对于body定位。

### 相对定位

相对定位是相对于该元素的本身，相对于自己原来位置的定位。他并不会使元素脱离文档流，只是多了一个可以为其设置位置坐标的功能

### 固定定位

fixed是相对于浏览器的视口进行定位，他不会随着滚动条的滚动而移动，是固定在浏览器的窗口上某个位置的。比如是小广告、性感荷官在线发牌。

## z-index

是用来调整定位时重叠块的上下位置，是相对于垂直于平面的z轴来说的。属性值是具体数字，数字越大的就在越上面。使用的元素需要是定位之后的元素。

## 定位布局方

### 固定浮动布局

- 不随窗口的变化而变化。
- 主要是使用float进行布局。
- 缩放窗口不会影响网页布局。
- 采用margin:0 auto;方式进行居中。

具体示例参看我的主页定位1

### 固定定位布局

- 不随窗口的变化而变化。
- 主要是使用position:absolte;进行布局。
- 缩放窗口不会影响网页布局。
- 采用position:absolute;拉回方式进行居中。

## 补充

### float和position的相互影响

如果在float上设置position：absolute的话，会覆盖float的属性。就不是浮动了,即float失效.

在float上设置position：relative的话，如果设置left/top/right/bottom等属性，则元素会先浮动到相应位置，然后再根据top/left/bottom/right所设置的距离发生偏移

在float上设置margin属性也是有效的。

### 两边固定，中间自适应布局

````html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
		<style type="text/css">
			#one{
				width: 200px;
				height: 500px;
				background-color: yellow;
				float: left;
			}
			#three{
                            width:200px;
				height: 500px;
				background-color: #0000FF;
				float:right;
	 		}
                      #two{
                                height:500px;
                                overflow:hidden;
                                background-color:black;
                            } /*两边固定，中间自适应*/
		</style>
	</head>
	<body>
		<div id="one">
			
		</div>
		<div id="three">
			
		</div>
             <div id="two">
			
		</div>
	</body>
</html>

````





