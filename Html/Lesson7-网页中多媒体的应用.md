# 第七课 网页中多媒体的应用

## 图片

- 插入图片的基本语法

  ````html
  <img src="URL" border="1" height="" width="" align="" alt=" " title=""> 
  ````

- 语法说明

  - src：**引入**的图片的路径，可以是相对路径也可以是绝对路径。
  - border：边框的粗细，可以选择不使用此项；用数字表示大小，单位是像素。
  - width&height：宽和高，单独设置其中一项时，其对应项会随之改变，图片本身比咧不会改变；设置两项时，图片会按照你给的比例变形。可以使用像素来调整其大小，也可以使用％来确定其大小，100%表示其父元素宽度的百分比（例如图片包含在\<body>...\<body>之内时，其父元素就是\<body>）。
  - align：对齐方式，*使用时会导致图片脱离文档流；如果想要其居中，可使用\<center>标记，或者使用<h#>标记，将图片认为是标题再利用标题中的属性对图片位置进行调整。*
  - title：鼠标滑到图片上面的提示字。
  - alt：图片加载失败时候的提示字。

## 背景音乐

\<bgsound>现在的主流浏览器中只有IE浏览器支持，且使用时没有控件控制，几乎不使用，故不做介绍。

## video

- 基本语法

  ````html
  <video src="url" controls>.....</video>
  ````

- 语法介绍

  src：引用的路径，可以为相对路径也可以是绝对路径。

  autoplay：自动播放。

  width&height：宽和高，单独设置其中一项时，其对应项会随之改变，视频本身比咧不会改变；改变其中两项时，视频比例不会变适应其中最小值。

  loop：循环次数，不设置此项时只播放一遍；如果设置该属性，则视频将循环播放。

  preload：预下载，视频在页面加载时进行加载，如果使用“autoplay”，则会忽略。

- 适用格式

  \<source>标签使用方法

  ````html
  <video width="320" height="240" controls>
      <source src="/images/video/demo.mp4" type="video/mp4">
      <source src="/images/video/demo.ogg" type="video/ogg">
       <source src="/images/video/demo.WebM" type="video/WebM">
      您的浏览器不支持video标记。
  </video>
  ````

  - MP4 = 具有H264视频编解码器和AAC音频编解码器的MPEG4文件

  - WebM = 具有VP8视频编解码器和Vorbis音频编解码器的WebM文件

  - Ogg = 带有Theora视频编解码器和Vorbis音频编解码器的Ogg文件

    ![image-20201030103904233](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201030103904233.png)

## audio

和video相似。

所支持格式wav、mp3、ogg

![image-20201030105516779](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201030105516779.png)

## canvas画布

**是HTML5新增的最重要的，且功能最强大的一个标记。主要用途有如下：**

- **绘制图像**
- **渲染文字**
- **制作动画**
- **制作游戏**

基本语法：\<canvas>.......\</canvas>。

语法说明：**块级**，默认画布大小为宽300px，高150px，有**且仅有这两个属性**。通过\<vanvas>的众多接口，由JavaScript控制。

## 补充内容

**href和src的区别：同样后面跟路径但是href意为指向资源；而src意为引入资源。**

