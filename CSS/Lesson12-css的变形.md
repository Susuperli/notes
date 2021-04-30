# 第十二讲 css的变形

## 变形

transform属性

css3新增的transform属性，可用于元素的变形，实现元素的旋转、缩放、移动、倾斜等变形效果。

- 基于webkit内核的替代私有属性：-webkit-transform

- 基于gecko内核的替代私有属性：-mo2-transform

- 基于presto内核的替代私有属性：-o-transform

- 基于trident内核的替代私有属性：-ms-transform.

基本语法：transform:none|transform-functions();

说明：none：是默认值，不设置变形。transform-functions()指的是变形函数。

### 2D变形

- rotate();旋转

  语法格式：transform:rotate(30deg);正数表示顺时针旋转，负数表示逆时针旋转。

- scale();放缩

  语法格式：transform:scale(x,y);表示中心放缩，其中x是指水平方向，y是指垂直方向。里面的内容也会随之进行放缩。

- translate();移动

  语法规则：transform:transform:translate(100px,100px);用于表示元素在二维空间的偏移。dx表示在水平方向，dy表示在垂直方向。可以是正数也可以是负数。

- skew();倾斜

  语法规则：transform:skew(anglex,angley);用于定义元素在二维空间的倾斜变形。参数表示在x轴和y轴上面的倾斜角度，按中心倾斜，单位是deg。

- transform-origin:x y;设置旋转中心。

  说明：x和y的默认值是50％，也就是元素的中心位置，设置新的旋转中心，可以使用%的形式，也可以是使用。
  
  效果举例
  
  `````html
  
  <!DOCTYPE html>
  <html>
  	<head>
  		<meta charset="utf-8">
  		<title></title>
  		<style type="text/css">
  			div{
  				margin: 50px;
  				width: 100px;
  				height: 100px;
  				border:black solid 1px;
  				text-align: center;
  				line-height:84px;
  				transform:rotate(30deg);
  				/*transform:scale(1,2);*/
  				/*transform:translate(100px,100px);*/
  				/*transform:skew(0,10deg);*/
  				transform-origin:x:left y:middle;
  			}
  			/*div:hover{
  				transform:translate(100px,100px)
  				/*background-color:red;
  			}*/
  		</style>
  	</head>
  	<body>
  		<div class="one">.</div>
  	</body>
  </html>
  
  `````

### 3D变形

- rotate3d(x,y,z,a);3D旋转。

  其中x是指的0-1之间的数值，表示旋转轴x方向的矢量（设置是否沿着x轴旋转）；y和z亦同之；a表示旋转角度，单位是deg。

  也可以分开写，rotateX(x) rotateY(y) rotateZ(z);可以写出里面的任意个。

- scale3d(sx,sy,sz);缩放。

  可以分开写，表示某一方向的放缩，scaleX(x) scaleY(y) scaleZ(z);

- translate3d(tx,ty,tz);移动。

  translateX(x) translateY(y) translateZ(z);

- transform-style:flat(默认)|preserve-3d;

  transform-style属性是指嵌套元素是怎样在三维空间中呈现。flat表示所有子元素都在2D中呈现。（**加到父元素中**），preserve-3d 表示所有子元素在3D空间中呈现。。

- perspective:number(eg:200px)|none;

  **景深**，规定3D元素的透视效果，多少像素的3D元素是从视图的perspective属性定义（加到父元素），这个属性允许你改变3D元素是怎样查看视图。他是一个元素的**子元素**透视图，而不是元素本身。只影响3D旋转元素。

- perspective-origin:x-axis y-axis;默认值是50％。

  perspective-origin属性定义3D元素所基于的x轴和y轴，该元素允许您改变3d元素的底部信息（**加到父元素**）。

  定义时的perspective-origin属性，他是一个元素的子元素，透视图而不是元素本身。


## 补充内容

### 对于景深**perspective**的理解

**对于景深perspective对于自己，只在最外层加一次？**景深的概念是在调焦使影像清晰时,在焦点的前后有一段距离内的区域,能够清晰显现,而这一段范围我们称之为*景深*

参见博客https://www.cnblogs.com/yanggeng/p/11285856.html

​      简单来说，就是设置这个属性后，那么，就可以模拟出像我们人看电脑上的显示的元素一样。比如说， perspective：800px  意思就是，我在离屏幕800px 的地方观看这个元素。(**这个属性，要设置在父元素上面**)

![perspetive](D:\0-Link\naotes\CSS\picture\perspetive.png)

先来看看， 加了perspective 和 没有加是什么区别， 第一个小方块，是有加的效果，能明显的看到空间感了有没有， 感觉他是真的像在旋转， 而第二个呢，像是在伸缩。

![perspective2](D:\0-Link\naotes\CSS\picture\perspective2.gif)

那么思考一个问题，transform：translateZ 呢，可以增加 Z轴的距离， 那么Z轴越大，是不是也就代表着，这个元素，离我们的距离越近？ 那么，你把一张图片，贴到你脸上，有什么效果？ 是不是非常大？有人可能会问，这两者之间有什么关系吗？ 肯定是有的，这个 perspective 配合 transform：translateZ 就有这种效果， 我们来看看。(先记着，我们设置了perspective：800px，那么来看看 Z到800px 有什么效果)

![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801222956571-567878966.gif)

 

有没有发现，临近 800px 的时候， 图片突然变黑了， 然后到800px的时候， 图片消失了。 这又是为啥呢？  其实很像我们现实中的例子一样，一张远处的图片，慢慢的移动到你脸上， 你会看见图片越来越大，贴到你脸上的时候，是不是 你就看不见了？ 到800px 的时候，你人都和图片 融合在一体了， 如果801px 是不是你都穿过这张图片了？道理是一样的啦。

 

那么transform：translateZ， 到负数的时候， 是不是值越小，图片离我们越远，同理的 图片也就越小。

![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801224057610-1784556030.gif)

 

但是！如果你真的认为 perspective 这个属性这么简单的话，那么你就太天真了。按照我们的思路继续，如果 perspective： 这个值，越小，是不是我们就离屏幕越近， 那么 图片也会越大，(translateZ 是移动图片， perspective是移动 人 和屏幕的距离，这么想也是没问题的哈。对吧，那么把translateZ(0px)。然后增加 perspective 试试看。 )

![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801225520468-1941953896.gif)

然后，你会惊奇的发现，咦？ 好像无论是增加，还是减少，图片都没有任何变化。 这个时候，先卖个关子，接着看下个案例，把 translateZ(-100px) 设置成 负值。(正常，按照我们的想法，是不是 Z的值是正数，说明这个图片，离我们越近，那么反之，负值，离我们越远对吧) 那么这次我们不移动 translateZ 了， 设置好Z 值为-100px 之后，移动perspective的值，把他的值变小，(正常来说，值越小，是不是就代表 我们离屏幕越近， 看的东西也就越大对吧)

![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801230607960-2031990058.gif)

然后，你又会惊奇的发现， 怎么图片不是越来越大呢? 我们离屏幕越大，图片应该越大才对啊， 怎么变小了呢？ 

其实把。这里我们一直误导一个情况，我们看到的，并不是图片本身，而是图片的投影。 是不是有点晕了，投影是什么鬼， 没事，看下面的图解。

 

第一个情况，translateZ 的值越大，图片越大。

 ![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801234131287-970705813.png)

 

第二个情况，translateZ 的值越小，图片越小。

![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801234818111-1640872733.png)

 

第三个情况，translateZ 为0的时候，为什么移动我们perspective 的值，图片的大小没有改变呢？

![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801232932435-607269886.png)

 

第四个情况，为什么translateZ 为负数之后，增加 perspective 的值后，图片不是变大， 反而变小呢？

 ![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801233508948-1693095665.png)

 

好了，最后补充一点，这个perspective 属性呢，要放在父级身上。然后还有一个属性perspective-origin，这个属性也是设置在父级身上。

这个属性呢，默认值是 center center，也就是 居中。这两个参数呢，是根据自身来定位的， 0px 0px 代表着元素的左上角，center center代表着元素的中间点。可以设置像素 50px 也可设置百分比 50%，还可以设置 top right left bottom center 等。

这个属性有什么用呢？ 这个属性是相当于人 的眼睛看哪里。你没有设置，也就是默认看父元素 中间的地方。看下面两张图的例子，就知道什么意思啦。

![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801235429754-139196392.png)

![img](https://img2018.cnblogs.com/blog/1609428/201908/1609428-20190801235955684-2042643681.png)

 