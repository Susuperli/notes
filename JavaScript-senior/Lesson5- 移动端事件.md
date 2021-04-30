# 第五讲  移动端事件

## H5新增事件

### 表单相关事件

- onblur：元素失去焦点。
- onchange：用户改变域的内容。
- onfocus：元素或得焦点。
- onsubmit：提交按钮被点击。
- onreset：重置按钮被点击。

### 文档加载事件

- onerror：当加载文档或图像时发生某个错误。
- onload：某个页面或图像被完成加载。
- onresize：窗口或框架被调整尺寸。
- onunload：用户退出页面。

### 新增事件

- onformchange：在表单改变时运行脚本(不兼容)。
- onforminput：当表单或得用户输入运行的脚本（不兼容）。
- oninput：当元素或得用户输入时运行的脚本。
- oninvalid：当元素无效时运行的脚本。

## touch事件

- touchstart：触摸开始时触发。
- touchmove：手指在屏幕上滑动的时候触发。
- touchend：触摸结束的时候触发。
- touchcance

touch事件使用监听的方式来绑定addEventListener('touchu事件',function(){})

````js
    var t=document.getElementById("test");
    t.addEventListener("touchstart",function(){
        t.style="background:red;"
    })
    t.addEventListener("touchmove",function(){
        console.log(2)
    })
    t.addEventListener("touchend",function(){
        console.log(3)
    })
````

## touch列表

每个触摸事件都包含了三个触摸列表，每个列表里办函了对应的一系列触摸点。

- touches：屏幕上的所有手指的一个列表。
- targetTouches：当前dom元素上的手指的一个列表。
- changedTouches：设计当前事件的手指的一个列表。

触摸列表都是数组对象，当中储存了每个触摸点的信息。

- clientY：相对于浏览器的窗口
- pageY：相对于dom页面来说, pageY和clientY的区别在于当页面超出一个屏幕的时候，pageY更大，pageY是相对于dom来说的。
- screenY: 相对于屏幕来说的，以左上角为原点进行计算。
- identifier:标识触摸会话中的当前手指的id。
- target：触摸的dom节点目标。

### 手势事件

目前还只是原型阶段

- gesturestart：当一个手指已经按在屏幕上，而另一个手指又触摸在屏幕时触发。
- gesturechange：当触摸屏幕的任何一个手指的位置放生变化时触发。
- gestureend：当任何一个手指从屏幕上面移开时触发。