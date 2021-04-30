# 第五课 列表

## 列表简介

以条目的形式有序或无序排列而形成的表

## 无序列表

- 是指一个没有特定顺序的相关条目的集合

- 基本语法

  ````html
  <ul type="circle">
      <li>华为</li>
      <li type="square">苹果</li>
      <li>小米</li>
  </ul>
  ````

- 语法说明：使用无序列表的type属性可以为前面符号的样式

  - disc：指定为一个实心圆。
  - circle：指定为一个空心圆。
  - square：指定为一个实心方框。

- \<ul>中只可以嵌套\<li>；而\<li>中可以嵌套任何标记

- 示例效果展示

  ![image-20201027163923483](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201027163923483.png)

## 有序列表

- 是一个特定顺序的相关条目（也称列表项）的集合。在有序列表中各个列表有先后顺序之分，他们之间以标号标记。

- 基本语法

  ````html
  <ol type="1">
      <li>华为</li>
      <li type="a">苹果</li>
      <li>小米</li>
  </ol>
  ````

  运行结果

  ![image-20201028082259350](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028082259350.png)

- 语法说明

  - type有以下五种计数方法

    - 1，阿拉伯数字依次计数。
    - a，小写字母依次计数。
    - A，大写字母依次计数。
    - i，小写罗马数字依次计数。
    - I，大写罗马数字依次计数。

  - start属性，可以规定从那个数开始计算，如：

    ````html
         <ol type="1" start="3">
                  <li>华为</li>
                  <li  type="a">苹果</li>
                  <li>小米</li>
       </ol>
    ````

    ![image-20201028083138901](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028083138901.png)

  - value属性，**表示从此处用几开始计算**，**只识别数字。**
  
    ````html
         <ol type="1">
                         <li>华为</li>
                         <li value="1">苹果</li>
                         <li>小米</li>
         </ol>
    ````
    
    运行结果显示
    
    ![image-20201028085021881](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028085021881.png)
    
  - 在\<ol>和\<li>中的属性发生冲突时，**就近原则**。

## 定义列表

没有项目符号，也没有标号，是通过缩进的形式使内容和层次更加清晰，**本身没有任何属性。**

基本语法

````html
<dl>
    <dt>One piece</dt>
    <dd>路飞</dd>
    <dd>娜美</dd>
    <dd>索隆</dd>
    <dd>山治</dd>
    <dt>火影忍者</dt>
    <dd>鸣人</dd>
    <dd>佐助</dd>
    <dd>小樱</dd>
    <dd>鹿丸</dd>
</dl>
````

运行结果展示

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028091430472.png" alt="image-20201028091430472" style="zoom: 80%;" />

## 菜单列表和目录列表（用得少）

​              **这两种列表和无序列表相似，故而用的少。**

- 菜单列表

  ````html
  <menu>
      <li>苹果</li>
      <li>橘子</li>
      <li>香蕉</li>
  </menu>
  ````

  ![image-20201028094407622](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028094407622.png)

- 目录列表

  ````html
  <dir>
      <li>苹果</li>
      <li>橘子</li>
      <li>香蕉</li>
  </dir>
  ````

  ![image-20201028094531385](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201028094531385.png)

## 嵌套规则

- 列表可以嵌套使用，也就是一个列表中可以包含很多层的子列表。
- 再网页文件中，对于内容层次较多的情况，使用嵌套列表不仅使网页的内容更加合理美观，而且使其内容看起来更加清晰明了。
- 嵌套的列表可以是无序列表的嵌套，也可以是有序列表的嵌套，还可以是无序列表和有序列表的混合嵌套。
- 嵌套的列表默认是缩进**40px**。



