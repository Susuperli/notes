# 第十一讲 css布局2-媒体查询和弹性盒子布局

## viewport简介

参考教程：[viewport 深入理解 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/viewport-deep-understanding.html)

### 概念

通俗的讲，移动设备上的viewport就是设备的屏幕上能用来显示我们的网页的那一块区域，在具体一点，就是浏览器上(也可能是一个app中的webview)用来显示网页的那部分区域，但viewport又不局限于浏览器可视区域的大小，它可能比浏览器的可视区域要大，也可能比浏览器的可视区域要小。

### css中1px的真实概念

css中的像素只是一个抽象的单位，在不同的设备或不同的环境中，css中的1px所代表的设备物理像素是不同的。在为桌面浏览器设计的网页中，我们无需对这个津津计较，但在移动设备上，必须弄明白这点。在早先的移动设备中，屏幕像素密度都比较低，如iphone3，它的分辨率为320x480，在iphone3上，一个css像素确实是等于一个屏幕物理像素的。后来随着技术的发展，移动设备的屏幕像素密度越来越高，从iphone4开始，苹果公司便推出了所谓的Retina屏，分辨率提高了一倍，变成640x960，但屏幕尺寸却没变化，这就意味着同样大小的屏幕上，像素却多了一倍，这时，一个css像素是等于两个物理像素的。其他品牌的移动设备也是这个道理。例如安卓设备根据屏幕像素密度可分为ldpi、mdpi、hdpi、xhdpi等不同的等级，分辨率也是五花八门，安卓设备上的一个css像素相当于多少个屏幕物理像素，也因设备的不同而不同，没有一个定论。

### viewport理论

- visual viewport：浏览器的可视区域。
- layout viewport：默认视图，实际宽度是大于浏览器可视区域宽度。
- ideal viewport：用于适配移动设备的理想宽度。

### 利用meta标签对viewport进行控

移动设备默认的viewport是layout viewport，也就是那个比屏幕要宽的viewport，但在进行移动设备网站的开发时，我们需要的是ideal viewport。那么怎么才能得到ideal viewport呢？这就该轮到meta标签出场了。

我们在开发移动设备的网站时，最常见的的一个动作就是把下面这个东西复制到我们的head标签中：

```html
<head>
      <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
</head>
```

该meta标签的作用是让当前viewport的宽度等于设备的宽度，同时不允许用户手动缩放。也许允不允许用户缩放不同的网站有不同的要求，但让viewport的宽度等于设备的宽度，这个应该是大家都想要的效果，如果你不这样的设定的话，那就会使用那个比屏幕宽的默认viewport，也就是说会出现横向滚动条。

**在苹果的规范中，meta viewport 有6个属性(暂且把content中的那些东西称为一个个属性和值)，如下：**

| width         | 设置***layout viewport*** 的宽度，为一个正整数，或字符串"width-device" |
| ------------- | ------------------------------------------------------------ |
| initial-scale | 设置页面的初始缩放值，为一个数字，可以带小数                 |
| minimum-scale | 允许用户的最小缩放值，为一个数字，可以带小数                 |
| maximum-scale | 允许用户的最大缩放值，为一个数字，可以带小数                 |
| height        | 设置***layout viewport*** 的高度，这个属性对我们并不重要，很少使用 |
| user-scalable | 是否允许用户进行缩放，值为"no"或"yes", no 代表不允许，yes代表允许 |

这些属性可以同时使用，也可以单独使用或混合使用，多个属性同时使用时用逗号隔开就行了。

此外，在安卓中还支持 target-densitydpi 这个私有属性，它表示目标设备的密度等级，作用是决定css中的1px代表多少物理像素

| target-densitydpi | 值可以为一个数值或 high-dpi 、 medium-dpi、 low-dpi、 device-dpi 这几个字符串中的一个 |
| ----------------- | ------------------------------------------------------------ |
|                   |                                                              |

特别说明的是，当 target-densitydpi=device-dpi 时， css中的1px会等于物理像素中的1px。

因为这个属性只有安卓支持，并且安卓已经决定要废弃 ~~target-densitydpi~~ 这个属性了，所以这个属性我们要避免进行使用 。

## 媒体查询

### 概念

通过不同的媒介类型和条件定义样式表规则，媒介查询让css可以更精确作用于不同的媒介类型和同一媒介的不同条件中，媒介查询的大部分媒介特性都接受min和max用于表达“大于或等于”和“小于或等于”IE9及其以下支持。

### 语法规则

- @media [only] mediatype and|not (media feature){css-code}

- 说明：mediatype表示媒体类型，也就是我们的样式使用在哪里。目前支持的类型有print打印机和打印预览；screen用于电脑屏幕、平板、智能手机；speech用于屏幕阅读器等发音设备；all用于所用的设备。其中screen类型最为常见用于电脑屏幕上。

  only：可选，只用于一种设备上。

  and|not：逻辑运算条件。

  media feature：表示媒体查询的功能。

  列举如下：

  ````html
  <style>
          @media screen and (min-width:1200px){
              div{
                  width: 100px;
                  height: 100px;
                  background-color: blue;
              }
          }
  </style>
  ````

  表示只在屏幕宽度在1200px之上显示。

- 媒介查询的方式除了加载css代码中，还可以在引用css文件时写入，作为link标记，写在style之后。

  ````html
  <style>
      div{
          width:60px;
          height:60px;
          border:1px solid red;
      }
  </style>
  <link type="text/css" rel="stylesheet" href="css.css" media="screen and (min-width:600px)">
  ````

  注：在css.css文件中不用在标记出@media，正常些css样式即可。

## 响应式开发原理

### 响应式

响应式web设计不仅仅是关于屏幕分辨率的自适应以及自动缩放的图片等等，它更像一种对于设计的全新思维模式，向下兼容，移动优先。

### 开发原理

参考博客：[响应式开发及其原理 - 澎湃_L - 博客园 (cnblogs.com)](https://www.cnblogs.com/EricZLin/p/9342762.html)

### rem

- rem是通过根元素（HTML）进行适配。

  是以根元素font-size大小为标准，rem是指其倍数。

  ````html
  	<style type="text/css">
  		@media screen and (min-width:320px){
  			html{
  				font-size:100px;
  			}
  		}
  		@media screen and (min-width:375px){
  			html{
  				font-size:px;
  			}
  		}
  		@media screen and (min-width:414px){
  			html{
  				font-size:px;
  			}
  		}
  		@media screen and (min-width:768px){
  			html{
  				font-size::px;
  			}
  		}
  		@media screen and (min-width:1024px){
  			html{
  				font-size::px;
  			}
  		}
  		div{
  			width: 10rem；
  			height: 10rem；
  		}
  	</style>
  ````

- rem的兼容性

- 以屏幕640为标准的rem算法

## 弹性盒子

参考：[CSS3 弹性盒子 | 菜鸟教程 (runoob.com)](https://www.runoob.com/css3/css3-flexbox.html)

### 弹性盒子简介

- **CSS3 弹性盒（ Flexible Box 或 flexbox），是一种当页面需要适应不同的屏幕大小以及设备类型时确保元素拥有恰当的行为的布局方式。**引入弹性盒布局模型的**目的**是提供一种更加有效的方式来对一个容器中的子元素进行排列、对齐和分配空白空间（IE浏览器中只有IE11支持，移动端都可以支持），弹性盒子由**弹性容器**(Flex container)和**弹性子元素**(Flex item)组成。

- 对与块级元素使用：display:flex;即可。

  对于行内元素使用：display:inline-flex;。

  兼容性：display:-webkit-flex;。

r任何元素都可以成为弹性元素，只能给外面的div设置display:flex;里面的项目会变成内容的大小，水平排列，可设置项目的大小。

**注意**，设为 Flex 布局以后，子元素的float、clear和vertical-align属性都将失效!!!

### 属性

#### 弹性容器属性

- flex-direction：决定主轴的方向（即项目的排列方向）
  - row：横向从左到右排列（左对齐），默认的排列方式。
  - row-reverse：反转横向排列（右对齐，从后往前排，最后一项排在最前面。
  - column：纵向排列。
  - column-reverse：反转纵向排列，从后往前排，最后一项排在最上面。
  
- flex-wrap：定义一条轴线，说明如何换行。
  - nowrap - 默认， 弹性容器为单行。该情况下弹性子项可能会溢出容器。
  - **wrap - 弹性容器为多行。该情况下弹性子项溢出的部分会被放置到新行，子项内部会发生断行**
  - wrap-reverse -反转 wrap 排列。
  
- flex-flow：该属性flex-direction属性和flew-wrap属性的简写模式，默认是row nowrap（**建议这么写**）。

- justify-content：定义的是项目在主轴方向的对齐方式。

  - flex-start：

    弹性项目向行头紧挨着填充。这个是默认值。第一个弹性项的main-start外边距边线被放置在该行的main-start边线，而后续弹性项依次平齐摆放。

  - flex-end：

    弹性项目向行尾紧挨着填充。第一个弹性项的main-end外边距边线被放置在该行的main-end边线，而后续弹性项依次平齐摆放。

  - center：

    弹性项目居中紧挨着填充。（如果剩余的自由空间是负的，则弹性项目将在两个方向上同时溢出）。

  - space-between：

    弹性项目平均分布在该行上。如果剩余空间为负或者只有一个弹性项，则该值等同于flex-start。否则，第1个弹性项的外边距和行的main-start边线对齐，而最后1个弹性项的外边距和行的main-end边线对齐，然后剩余的弹性项分布在该行上，**相邻项目的间隔相等**。

    ````html
    <style>
        div{
                border: solid 1px red;
                display: flex;
                height: 500px;
    	     justify-content:space-between;
            } 
    </style>
    ````

    ![image-20201130153026709](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201130153026709.png)

  - space-around：

    - 弹性项目平均分布在该行上，两边留有一半的间隔空间。如果剩余空间为负或者只有一个弹性项，则该值等同于center。否则，弹性项目沿该行分布，且彼此间隔相等（比如是20px），同时首尾两边和弹性容器之间留有一半的间隔（1/2*20px=10px）

      ![image-20201130153149718](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201130153149718.png)

  - align-items：属性定义项目在交叉轴（**垂直轴**）如何对齐。

    - flex-start：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
    - flex-end：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
    - center：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
    - baseline：如弹性盒子元素的行内轴与侧轴为同一条，则该值与'flex-start'等效。其它情况下，该值将参与基线对齐。
    - stretch：即使未设置宽高也会沾满整个屏幕，如果指定侧轴大小的属性值为'auto'，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照'min/max-width/height'属性的限制

  - 现在提供新的对齐方式

    `````html
    <style>
        div{
                border: solid 1px red;
                display: flex;
                height: 500px;
    	     justify-content:center;
                align-items:center;
            } 
    </style>
    `````

    ![image-20201130155419197](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201130155419197.png)

    

#### 项目属性

- order：\<integer>：用整数值来定义排列顺序，数值**小**的排在**前面**。可以为负值。

- flex-grow：定义项目的放大比例，默认是0，即右边有剩余空间也不会放大。

- flex-shrink：定义 了项目的缩小比例，默认是1，即空间不足时，容器内的所有子元素都会同比例缩小；如果一个是0，另外两个是1，那么空间不足时，第一个不会缩小后面两个会同比例缩小。

- **flex-basis：？**

- flex

  | 值            |                             描述                             |
  | :------------ | :----------------------------------------------------------: |
  | *flex-grow*   |    一个数字，规定项目将相对于其他灵活的项目进行扩展的量。    |
  | *flex-shrink* |    一个数字，规定项目将相对于其他灵活的项目进行收缩的量。    |
  | *flex-basis*  | 项目的长度。合法值："auto"、"inherit" 或一个后跟 "%"、"px"、"em" 或任何其他长度单位的数字。 |
  | auto          |                      与 1 1 auto 相同。                      |
  | none          |                      与 0 0 auto 相同。                      |
  | initial       |           设置该属性为它的默认值，即为 0 1 auto。            |
  | inherit       |                     从父元素继承该属性。                     |





