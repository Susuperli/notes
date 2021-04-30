# 第五讲 使用css文件设置超链接

## 去除超链接下划线

text-decoration:none|underline|overline|line-through;

可以使用此语句来去除或是增加下划线。

## 超链接动态

使用伪类选择器去创建动态超链接。

a:link 鼠标点击前的样式。

a:visited 被点击过的超链接的样式。

a:hover 鼠标指针经过超链接时的样式。

a:active 鼠标激活状态下的样式，即点击过程中超链接的状态。

注意：书写顺序，link→visited→hover→action。随意打乱书写顺序的话会发生预期之外的错误。一般是将link和visited的样式写在一块a:link,a:visited，一般会省略active的样式。

## 鼠标特效

css可以通过如下语句控制光标的形状。

cursor:属性值;写在伪类控制器里面。

属性值如下：

![image-20201112162448407](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201112162448407.png)

