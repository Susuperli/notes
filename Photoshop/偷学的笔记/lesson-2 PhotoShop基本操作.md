# lesson-2 PhotoShop基本操作

## **photoshop快捷键**



|  常用功能  | 快捷键     |
| :--------: | ---------- |
|    打开    | ctrl+O     |
|    新建    | ctrl+N     |
|    标尺    | ctrl+R     |
| 填充前景色 | AIL+DEL    |
| 填充背景色 | CTRL+DEL   |
|  取消选区  | CTRL+D     |
|    撤销    | CTRL+ALT+Z |
| 隐藏参考线 | CTRL+；    |
|  抓手工具  | H          |



## **网页效果图 相关常识** 

![mark](http://qiniu.wind-zhou.com/blog/20201013/v8EeaOG1gXXo.png?imageslim)

宽度一般**1920px**，高度一般不限制（由内容决定）。

颜色模式选RGB，CMYK为印刷时使用。

分辨率一般为72ppi。



标尺用参考线辅助测量（移动工具帮助进行移动）。

shift+移动工具可以进行**整像素移动**。



## **photoshop存储格式**

- [x] PSD--PhotoshopDocument   

- 优点：PS中所有的信息都会被这种格式保存下来（例如图层，参考线），方便修改，但不支持超大图片（大于2G）。
- 缺点：占用空间大



- [x] jpg--全名JPEG 

- 优点：支持高级压缩（压缩比比较高），支持真色彩。

- 缺点：属于有损压缩，会损伤图像质量，不支持背景透明（Alpha）。

  > 背景透明含义（qq头像），如下：阴影部分为透明部分。
  >
  > ![mark](http://qiniu.wind-zhou.com/blog/20201013/fBX8LH2UBPvA.png?imageslim)



- [x] gif    
- 优点：属于无损压缩，体积小，成像相对清晰。支持动画，支持透明。
- 缺点：色彩较少，图像不多于256色，不支持Alpha通道（羽       化）。
- [x] png
-  优点：支持背景透明，羽化，采用无损压缩，支持真色彩。
- 缺点：相对较大，ie6浏览器下不支持。

![mark](http://qiniu.wind-zhou.com/blog/20201014/iXvReEAF5wmh.png?imageslim)



![mark](http://qiniu.wind-zhou.com/blog/20201014/DDkSYopsKwvd.png?imageslim)

## **建立选区**

![mark](http://qiniu.wind-zhou.com/blog/20201013/9E349Ggkcxt5.png?imageslim)

画正方形和正圆：shift+相应选区框。

在指定位置画正原：shift+alt+相应选区框。



**建立圆环的方法：**

1. 建立一个圆形选区
2. 使用在选区中减去，然后再在第一个圆中再画一个小圆

**羽化**：在选区边缘建立一个渐透明度的过渡区域（渐透明是选区内的颜色）。常用于发光效果或图像融合。**（先设置羽化值，再进行色彩填充。）**

当预设羽化值时，矩形选区的边缘将不是直角。

![mark](http://qiniu.wind-zhou.com/blog/20201013/sp5wyQajEXQQ.png?imageslim)



> 作业：找五个不同的网站并画出网站结构，存成psd格式。备注上相应网站，后缀名为“网站名称.psd”

