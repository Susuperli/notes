# lesson-4 颜色模式

颜色模式：颜色的生成方式，常用：RGB(常用),CMYK（印刷）,HSB（灯）

![mark](http://qiniu.wind-zhou.com/blog/20201016/H6pLY8mwiGu4.png?imageslim)

## RGB颜色模式

**原理**：光的三原色（神说：要有光）

**颜色的深浅靠发光亮度来表示。**

应用于所有的电子设备。

![mark](http://qiniu.wind-zhou.com/blog/20201016/78hm56P2fJzd.png?imageslim)

R--RED

G--GREEN

B--BLUE

红+绿=黄，绿+蓝=清，红+蓝=紫（洋红）

**补色（反色）的概念**：两种颜色相叠加为白色，则两种颜色互为补色。

例：红-----青，黄----蓝，紫-----绿。

应用：在调色时可以相应增加补色亮度进而削弱目标颜色。

**颜色的数值表示：** 

|   红   | rgb（255，0，0）或#FF0000       |
| :----: | ------------------------------- |
| **绿** | **rgb（0，255，0）或#00FF00**   |
| **蓝** | **rgb（0，0，255）或#0000FF**   |
| **黄** | **rgb（255，255，0）或#FFFF00** |
| **青** | **rgb（0，255，255）或#00FFFF** |
| **紫** | **rgb（255，0，255）或#FF00FF** |

> 常识：255=11111111=#FF

## CMYK颜色模式

**原理**：CMY--油墨的三原色（自己不发光，靠反射太阳光进行颜色显示）

颜色的深浅靠油墨的浓度来表示。用百分比衡量大小（0-100%）。

C--青色

M--洋红

Y--黄色

K--黑色

![mark](http://qiniu.wind-zhou.com/blog/20201016/gkuWTL7md6mx.png?imageslim)

**缺点**：颜色表现能力比较差，所能描绘的色彩亮较少。可表示100*100\*100种颜色。

现实案例为：打印出来的照片可能和电脑显示的颜色有色差（淘宝的商家经常这么干）。

有时为了消除色差，可以在ps中将RGB转换为CMYK（一般会变暗一些）。

![mark](http://qiniu.wind-zhou.com/blog/20201016/xfm9OaPPAhgc.png?imageslim)

此时查看通道便变成了CMYK模式。

![mark](http://qiniu.wind-zhou.com/blog/20201016/jOgvjAkF8XkL.png?imageslim)

**注：当换成CMYK再转成RGB时，丢失的颜色不会返回。**

**在转之前可以通过“色域警告”来预览一下有哪些色彩会丢失。**

![mark](http://qiniu.wind-zhou.com/blog/20201016/btwvx5MzB9HI.png?imageslim)

## HSB模式

![mark](http://qiniu.wind-zhou.com/blog/20201016/X01i7OYqJAl7.png?imageslim)

**靠人的肉眼对颜色的感知来定义的颜色模式。**

感知包括颜色的三种属性：

- **H--色相** 指的是色彩的固有属性（就是你是什么颜色的）。**注：黑，白，灰没有色相，只有亮度和明暗的变化，彩色才有色相**。

![mark](http://qiniu.wind-zhou.com/blog/20201016/pVmQ6DGcg3hg.png?imageslim)

- **S--饱和度**  颜色的强度或纯度，指的是颜色的鲜艳程度。

![mark](http://qiniu.wind-zhou.com/blog/20201016/yNyG6tPBGkzR.png?imageslim)

- **B--亮度**

![mark](http://qiniu.wind-zhou.com/blog/20201016/1pY8HQFCsoY1.png?imageslim)

ps中的HSB模式应用就是**拾色器**。

![mark](http://qiniu.wind-zhou.com/blog/20201016/hsrEpvDw1f6C.png?imageslim)

## 灰度模式

没有色相，只有黑白灰三种颜色。（一般用不到）

## 位图模式

只有黑白的颜色模式。（用于一些特殊效果的处理）

## 调色

###调节色阶

**色阶的概念**：图片的灰度级分布情况，而调整色阶就是改变一幅图的灰度分布情况，直观表现就是一幅图的明暗关系。快捷键：ctrl+L

![mark](http://qiniu.wind-zhou.com/blog/20201016/QLaCb0VC5lfH.png?imageslim)

>色阶的调节原理：通过移动左侧的调节按钮可以改变0亮度的像素点的个数。例如将左侧按钮拉至100处，则1亮度低于100的像素点（暗像素点）的亮度左都被置为0，此时呈现的效果是暗处更暗。同理将右侧拉至200处，那么亮度大于200的像素点（亮像素点）的亮度都将被置为255，此时呈现的效果是亮出更亮。通过亮暗的调节，可以改变图片的对比度，改善图片的视觉呈现效果。

**原图像：**![mark](http://qiniu.wind-zhou.com/blog/20201016/6dScsM7t8oIs.png?imageslim)

**调整色阶之后：**

![mark](http://qiniu.wind-zhou.com/blog/20201016/sCyeBs4KAduE.png?imageslim)

###调节**饱和度**

可以让天空更蓝(增加青色或蓝色的饱和度)。

![mark](http://qiniu.wind-zhou.com/blog/20201016/JP68U4MmVHwA.png?imageslim)

###调节色相

可以通过色相调整可以改变物体的颜色。

**原图：**

![mark](http://qiniu.wind-zhou.com/blog/20201016/9bk2stXWFp1e.png?imageslim)

**调节色相后的效果**：

![mark](http://qiniu.wind-zhou.com/blog/20201016/tb3oTcUOhftJ.png?imageslim)

这个例子中因为裙子的颜色恰好为青色，因此	调节，不过这种方法改变颜色感觉不太方便。

### 颜色替换

![mark](http://qiniu.wind-zhou.com/blog/20201016/9idBXOJdpEQd.png?imageslim)

这种是专业的颜色替换方法，适用于纯色或颜色变化小的图片。

**色彩平衡**：通过补色原理

![mark](http://qiniu.wind-zhou.com/blog/20201016/0NooIwVIqb3a.png?imageslim)

阈值：

阴影和高光：常用于调节逆光拍摄的图片

![mark](http://qiniu.wind-zhou.com/blog/20201016/mIRlGhpUenfL.png?imageslim)

这个没找到理想图片，自行体会吧！

## 扩展知识

###色域、色深等概念的理解

简单来说为了对所有颜色进行标准化，国际照明委员会（CIE）的颜色科学家们对人眼可见的颜色进行了统一的编码。如下图：

![mark](http://qiniu.wind-zhou.com/blog/20201013/sOGXfg82NO2u.png?imageslim)



然后三家单位分别在此基础上建立了一套各自的颜色空间标准，分别为sRGB、NTSC、AdobeRGB。

![mark](http://qiniu.wind-zhou.com/blog/20201013/leXbWLY1X5KA.png?imageslim)

色域顾名思义就是色彩的区域，简单来说就是表示颜色的丰富度。

显示器中的色彩是由RGB三种颜色（光的三原色）组合而成，每一种颜色有在计算机中都会进行相应编码，如果一种颜色用一个字节来表示（8bit），那么每种颜色的灰度等级便有256个，因此RGB组合出来的色彩区域便有256*\*256\*256种。这里的256就是色深。当然如果10位色深，那表示的颜色区域变为1024\*1024*1024。

> 相关链接：https://www.sohu.com/a/159406850_641165