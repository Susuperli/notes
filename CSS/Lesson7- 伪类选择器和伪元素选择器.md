# 第七讲 伪类选择器和伪元素选择器

## 结构伪类选择器

|       选择器        |                             描述                             | 版本 |
| :-----------------: | :----------------------------------------------------------: | :--: |
|        :root        |                   选择匹配所在文档的根元素                   | css3 |
|    E:first-child    | 匹配父元素的**第一个**的**子元素**E（**两个条件，第一个和子元素都需要满足**） | css3 |
|    E:last-child     |                 匹配父元素的最后一子个元素E                  | css2 |
|   E:nth-child(n)    |                   匹配父元素的第n个子元素E                   | css3 |
| E:nth-last-child(n) |                 匹配父元素的倒数第n个子元素E                 | css3 |
|    E:only-child     |                 匹配父元素仅有的一个子元素E                  | css3 |
|       E:empty       |          匹配没有任何子元素（包括文本节点）的元素E           | css3 |

| 选择器                | 描述                                      | 版本 |
| --------------------- | ----------------------------------------- | ---- |
| E:first-of-type       | 匹配同类型中的第一个匹配到的同级兄弟元素E |      |
| E:last-of-type        | 匹配同类型的最后一个匹配的同级兄弟E       |      |
| E:only-of-type        | 匹配同类型中的唯一一个匹配的同级兄弟E     |      |
| E:nth-last-type(n)    | 匹配同类型的第n个同级兄弟E                |      |
| E:nth-last-of-type(n) | 匹配同类型中的第n个同级兄弟E              |      |

- 对于所有nth中的n的值都是可以选择

  2n：偶数，2n+1奇数，3n以此类推..

  或是英文单词odd奇数，even偶数。

- first-child与:first-of-type的区别

  :first-child选择器是css2中定义的选择器，从字面意思上来看也很好理解，就是第一个子元素。比如有段代码：

  [![QQ截图20140210135428](https://images0.cnblogs.com/blog/130623/201402/261609103381767.png)](https://images0.c7nblogs.com/blog/130623/201402/261609099832424.png)

  p:first-child 匹配到的是p元素,因为p元素是div的第一个子元素；

  h1:first-child 匹配不到任何元素，因为在这里h1是div的第二个子元素，而不是第一个；

  span:first-child 匹配不到任何元素，因为在这里两个span元素都不是div的第一个子元素；

  :first-child 匹配到的是p元素,因为在这里div的第一个子元素就是p。

  

  然后，在css3中又定义了:first-of-type这个选择器，这个跟:first-child有什么区别呢？还是看那段代码：

  [![QQ截图20140210135428](https://images0.cnblogs.com/blog/130623/201402/261609112053896.png)](https://images0.cnblogs.com/blog/130623/201402/261609107566595.png)

  p:first-of-type 匹配到的是p元素,因为p是div的所有为p的子元素中的第一个，事实上这里也只有一个为p的子元素；

  h1:first-of-type 匹配到的是h1元素，因为h1是div的所有为h1的子元素中的第一个，事实上这里也只有一个为h1的子元素；

  span:first-of-type 匹配到的是第三个子元素span。这里div有两个为span的子元素，匹配到的是第一个。

  :first-of-type 匹配到的是p元素

   

  所以，通过以上两个例子可以得出结论：

  :first-child 匹配的是某父元素的第一个子元素，可以说是结构上的第一个子元素。

  :first-of-type 匹配的是该类型的第一个，类型是指什么呢，就是冒号前面匹配到的东西，比如 p:first-of-type，就是指所有p元素中的第一个。这里不再限制是第一个子元素了，只要是该类型元素的第一个就行了，当然这些元素的范围都是属于同一级的，也就是同辈的。

  同样类型的选择器 :last-child 和 :last-of-type、:nth-child(n) 和 :nth-of-type(n) 也可以这样去理解。

## 状态伪类选择器

|  选择器   |              描述               |      说明      |
| :-------: | :-----------------------------: | :------------: |
|  E:link   |       超链接访问前的样式        | **超链接专属** |
| E:visited |      超链接被访问后的样式       | **超链接专属** |
|  E:hover  |   设置元素在鼠标悬停时的样式    |                |
| E:active  |          激活时的样式           |                |
|  E:focus  |   设置元素在成为焦点时的样式    |                |
| E:checked | 匹配表单中，处于选中状态的元素E |                |
| E:enable  | 匹配表单中，处于禁止状态的元素E |                |

## 伪元素选择器

|             选择器             |                          描述                           |
| :----------------------------: | :-----------------------------------------------------: |
| E:first-letter/E::first-letter |              设置对象内的第一个字符的样式               |
|   E:first-line/E::first-line   |                 设置对象内第一行的样式                  |
|       E:before/E::before       | 设置对象前发生的内容与content属性一起使用（**行内式**） |
|        E:after/E::after        | 设置对象后发生的内容与content属性一起使用（**行内式**） |

**注：两个冒号是css3新的写法，用来区分伪类选择器（单冒号）和伪元素选择器。**

`````html
<style>
    p:before{
        content:"";
        display:inline-block;
        width:0px;
        height:0px;
         border:10px solid transparent;
        border-left-color:red;
    }
</style>
`````

在段落p之前插入一个小三角。

![image-20201115231136995](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201115231136995.png)

写入图片

````html
<style>
        h2:before{
            content:url(hot.gif);
        }
    </style>
````



## 属性选择器

|      选择器       |               描述                |
| :---------------: | :-------------------------------: |
|      E[attr]      |       选取拥有此属性的E元素       |
|  E[attr="value"]  |     选择属性值为value的E元素E     |
| E[attr^="value"]  |   选取属性值以value开始的元素E    |
| E[attr$="value"]  |   选取属性值以value结束的元素E    |
| E[attr*="value"]  |     选取属性值有value的元素E      |
| E[attr~="value"]  | 选取多个属性值中包含value的元素E  |
| E[attr\|="value"] | 选取指定属性具有指定值开始的元素E |

注：只写属性选择器[]，表示选择所有符合属性过滤选择器的元素。