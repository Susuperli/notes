# 第八讲 jQuery事件

## onload和ready的区别

- 执行时机都是在网页加载完成后调用

  onload必须等待网页中所有的内容加载完毕后（包括图片）；ready在网页中所有DOM解雇绘制完毕后就执行，可能与DOM关联的东西没有加载完成。

- 编写个数

  onload不能同时编写多个；ready可以同时编写多个。

- 简写方式

## 事件绑定方法

### bind()方法

bind("事件名称",处理函数)

````js
$("button").bind("click",function(){
  $("p").slideToggle();
});
````

unbind()，解除绑定方法

`````js
 $("button").click(function(){
    $("p").unbind();
  });
`````

### one()方法

one() 方法为被选元素附加一个或多个事件处理程序，并规定当事件发生时运行的函数。

当使用 one() 方法时，每个元素**只能运行一次**事件处理器函数。

````js
$("p").one("click",function(){
  $(this).animate({fontSize:"+=6px"});
});
````

### live()方法

live() 方法为被选元素附加一个或多个事件处理程序，并规定当这些事件发生时运行的函数**（1.9之后版本已删除）**。

通过 live() 方法附加的事件处理程序适用于匹配选择器的**当前及未来的元素（比如由脚本创建的新元素）。**

````js
$("button").live("click",function(){
  $("p").slideToggle();
});
````

die(),解除绑定方式。

### **on()方法**

on() 方法在被选元素及子元素上添加一个或多个事件处理程序。

自 jQuery 版本 1.7 起，on() 方法是 bind()、live() 和 delegate() 方法的新的**替代品**。该方法给 API 带来很多便利，我们推荐使用该方法，它简化了 jQuery 代码库。

**注意：**使用 on() 方法添加的事件处理程序适用于**当前及未来的元素（比如由脚本创建的新元素）。**

**提示：**如需移除事件处理程序，请使用 [off()](https://www.runoob.com/jquery/event-off.html) 方法。

**提示：**如需添加只运行一次的事件然后移除，请使用 [one()](https://www.runoob.com/jquery/event-one.html) 方法。

````JS
$(document).ready(function(){
  $("#div1").on("click",function(){
    $(this).css("background-color","pink");
  });
````

````js
$("ul").on("click","li",function(){})  //事件委托
````

## 事件类型

1,鼠标单击，双机事件

click ,dblclick

2,鼠标按下事件

mousedown,mouseup

mouseout,mouseover,mousemove,

3,表单事件

change,select,submit ,focus,blur

4,键盘按下事件

keyup，keydown,keypress

4,屏幕按下事件

load,resize,scroll,error

## 合成事件

**1.hover(enter,leave)**

hover方法用于模拟光标悬停事件.当光标移动到元素上时,会触发第一个函数,移出这个元素时,会触发第二个函数.**

```js
$(function(){
    $("#panel h5.head").hover(function(){
	    $(this).next().show();
	},function(){
            $(this).next().hide();   
	})
})
```


2.toggle(fn1,fn2,...fnN)

(1):模拟鼠标连续点击事件,第一个点击触发fn1,第二次触发fn2.......,随后轮番进行调用;

```js
$(function(){
    $("#panel h5.head").toggle(function(){
			$(this).next().show();
	},function(){
			$(this).next().hide();
	})
})
```

(2):toggle()切换元素的可见状态**

```js
   $("#panel h5.head").toggle(function(){
			$(this).next().toggle();
	},function(){
			$(this).next().toggle();
	})
```

## 事件对象

参考：https://www.jb51.net/article/123256.htm

js中事件是会导致冒泡的，所以this也是会变化的，但是event.target不会变化，它永远是直接接收事件的目标DOM元素。

this和event.target都是DOM对象，可以转化为jQuery对象。

````js
$("a").click(function(event) {
 alert(event.type); // "click"事件
});
````

**pageX和pageY获取的是距离页面原点的位置；screenX和screenY获取的是距离显示屏的位置；clientX和clientY获取的是距离页面视口的距离。在没有滚动条的时候，pageY和clientY在数值上是一样的。当有滚动条的时候，pageY会明显变大，因为它是相对于页面原点。**

![jq8](D:\0-Link\naotes\picture\jq8.png)

**阻止冒泡：**

如果在页面中重叠了多个元素， 并且重叠的这些元素都绑定了同一个事件， 那么就会出现冒泡问题。

示例：

**//HTML** **页面**

```js
1 <div style="width:200px;height:200px;background:red;">
2     <input type="button" value="按钮" />
3 </div>
```

```js
 1 //三个不同元素触发事件
 2 
 3 $('input').click(function () {
 4 
 5     alert('按钮被触发了！');
 6 
 7 });
 8 
 9 $('div').click(function () {
10 
11     alert('div 层被触发了！');
12 
13 });
14 
15 $(document).click(function () {
16 
17     alert('文档页面被触发了！');
18 
19 });
```

**PS：当我们点击文档的时候，只触发文档事件；当我们点击 div 层时，触发了 div 和文档两个；当我们点击按钮时，触发了按钮、div 和文档。触发的顺序是从小范围到大范围。这就是所谓的冒泡现象，一层一层往上。**

jQuery 提供了一个事件对象的方法：**event.stopPropagation()**；这个方法设置到需要触发的事件上时，所有上层的冒泡行为都将被取消。

$('input').click(function (e) {

　　alert('按钮被触发了！');

　　**e.stopPropagation();**

});

**阻止默认行为：**

网页中的元素，在操作的时候会有自己的默认行为。比如：右击文本框输入区域，会弹出系统菜单、点击超链接会跳转到指定页面、点击提交按钮会提交数据。

//阻止超链接进行跳转

$('a').click(function (e) { 

　　**e.preventDefault();**

});

//禁止提交表单跳转（注意是在form上阻止）

$('form').submit(function (e) {

　　**e.preventDefault();**

});

**PS： 如果想让上面的超链接同时阻止默认行为且禁止冒泡行为， 可以把两个方法同时写上： event.stopPropagation()和 event.preventDefault()。 这两个方法如果需要同时启用的时候，还有一种简写方案代替，就是直接 return false。**

$('a').click(function (e) {

　　**return false;**

});