#   第六课 超链接

## 超链接介绍

**是指从一个网页指向一个目标的连接关系，这个目标可以是另一个网页，也可以是相同网页上的不同位置。**

##  超链接分类

### 外部链接

​        所谓外部链接指的是跳转到当前网站的外部，与其它网站中页面或其他元素之间的连接关系，这种链接的URL地址一般要用绝对路径，要有完整的URL地址。

###  内部链接

​       内部链接指的是在同一个网站内部，不同的html页面之间的连接关系，在建立网站内部链接的时候，要明确哪个是主链接文件（即当前页），哪个是被链接文件相对路径，以当前文件所在的路径为起点，进行文件查找。

## 如何创建超链接

###  基本语法

````html
<a href="url" title="" target="目标窗口">链接名称</a>                        <!-- 行内标记-->
````

###  语法说明

- **href**：链接的属性，和URL结合设置这个链接**所指向的目标地址**。
- title：**用于鼠标指向连接时所显示的提示信息**。
- target：**用于指定打开链接的目标窗口**
  -  _self：在当前窗口打开，系统默认即使如此。
  -  _blank：在新窗口打开。

### 书签的其他用法

- 电子邮件链接（因为要安装特定的软件，不能确认访客电脑是否安装，故而用的少，了解即可。）

  基本语法：

  ````html
  <a href ="mailto:E-mail地址 ?subject=邮件主题 &参数=参数值">内容</a>
  ````

- **书签链接**（用的多）

  ​       在浏览页面时，如果页面的篇幅很长，要不断移动滚动条，给浏览带来不便。当浏览者单击页面上的某一书签时，就能跳转到网页的相应位置进行阅读，这相应的位置称之为锚。引入如下概念，

  - **锚链接**：顾名思义，意为在此次抛锚，在此处留下标记。

    基本语法：

    ````html
    <a name="书签名">链接标题</a>
    ````

  - 本页面书签链接使用格式：

    ````html
    <a href="#书签名称" target="目标窗口" >链接名称</a>
    ````

  - 不同页面使用书签链接的格式：

    ````html
    <a href="URL地址#书签名称" target="目标窗口">链接标题</a>
    ````

## 补充内容

###  相对路径和绝对路径

　   [绝对路径](https://www.baidu.com/s?wd=绝对路径&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjN-mvNWuW6dmWDdnv7b0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjTLnjfkPjfL)：绝对路径就是你的主页上的文件或目录在硬盘上真正的路径，(URL和物理路径)例如：
C:\xyz\test.txt 代表了test.txt文件的绝对路径。http://www.sun.com/index.htm也代表了一个
URL绝对路径。

　　[相对路径](https://www.baidu.com/s?wd=相对路径&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjN-mvNWuW6dmWDdnv7b0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjTLnjfkPjfL)：相对与某个基准目录的路径。包含Web的相对路径（HTML中的相对目录），例如：在
Servlet中，"/"代表Web应用的根目录。和物理路径的相对表示，例如："./" 代表当前目录，"../"代表上级目录。这种类似的表示，也是属于相对路径。

###  相对路径的找法

- 同一目录下的文件main.html ,href="main.html"
- 下一子级目录的web文件夹中的main.html，href="web/main.html"
- 上一级目录中main.html，href="../main.html"
- 上两级目录中main.html，href="../../main.html"
- **不可以跨盘符寻找**

