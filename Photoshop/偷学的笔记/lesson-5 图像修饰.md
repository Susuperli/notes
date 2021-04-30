# lesson-5 图像修饰

## **污点修复工具**

磨皮：

1. 先图像预处理（包括去痘印等）
2. 复制图层
3. 对复制图层进行高斯模糊
4. 点击历史记录，选择复制图层
5. 点中高斯模糊步骤前面的小方块（设置历史记录画笔的源）
6. 使用工具栏中的历史记录画笔在需要处理的地方进行处理。

磨皮之前：

![mark](http://qiniu.wind-zhou.com/blog/20201017/ER6PeY5o8uR6.png?imageslim)

磨皮之后：

![mark](http://qiniu.wind-zhou.com/blog/20201017/VzMLFWjTuvmr.png?imageslim)

>历史记录画笔的原理：历史记录画笔可以对涂抹区域进行某一部历史记录相同的操作。
>
>以上图为例，磨皮的原理就是对脸部进行高斯模糊。这里有两个条件一是模糊化，二是区域化。历史记录画笔起的作用就是区域化，之前进行高斯模糊只是为了让历史记录中存在这一步操作。（因为历史记录画笔需要结合历史记录进行使用）



## **修复画笔工具**

用于修复一些较大的疤痕，如条状疤痕。

原理是使用要修补部分周围的色彩对所修补部分进行颜色填充。

使用**ALT+鼠标左键**可以实现对填补颜色的采集。

**修补前：**

![mark](http://qiniu.wind-zhou.com/blog/20201017/lNu83qxPKhCe.png?imageslim)

**修补后：**

![mark](http://qiniu.wind-zhou.com/blog/20201017/yE5iNvdJrCmk.png?imageslim)

## **修补工具**

适用于背景单一图像中某一部分的去除。

处理前：

![mark](http://qiniu.wind-zhou.com/blog/20201017/Q91gtlfncOe4.png?imageslim)

**处理后：**

![mark](http://qiniu.wind-zhou.com/blog/20201017/dYBpdkSAQbjs.png?imageslim)

## **绘图工具**

- 画笔

  - 大小
  - 硬度（可以理解为羽化效果）

  **笔尖形状也可以自定义**

- 钢笔 （用来画轮廓）
  里面的线条是路径，辅助绘制轮廓，是矢量图，打印时不会显示

  路径有两种：平滑点和角点

  重要东西的有锚点，填充颜色，描边等。

  还有一个重要的是画形状。

  **这节不太重要，需要时再看吧！**

  

  



