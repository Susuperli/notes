# 第九讲 表单

## 表单

​       在网页中用来给访问者填写信息，从而获得用户信息使网页具有交互的功能，一般将表单设计在一个HTML文档中，当用户填写完信息后，表单的内容就从客户端的浏览器传送至服务器上，经过服务器的PHP文件或JSP等程序处理后，将用户所需信息传送至客户端的浏览器。

````html
<form name="html" action="" method="">
    <input>
    <select>
        
    </select>
    <textarea></textarea>
</form>
````

### 表单语法说明

- **name**：给定表单名称，表单名名之后就可以使用脚本语言（如js）对它进行控制。如果有多个表单时，提交到后台时便于识别不同的表单。（**必填**）

- **action**：提交处理表单信息的服务器端用的应用程序，可以是PHP或jsp等页面。（**必填**）

- **method**：该属性用于指定表单向服务器提交数据的方式，可以是get或是post，默认为get。

  - **get方法：使用get方法提交数据，浏览器将表单中各个值添加到action属性指定的URL后（两者之间用问号进行分割）并向服务器发送get请求，每个值之间用&链接。**

    - **get方法的缺点<u>：*地址栏允许输入的URL长度是有限制的，*</u>最多能允许传递的是2048个字符（不能大于2k），所以如果数据过大此方法不允许。提交数据后我们所提交的数据是明文。**

  - **post方法**

    **post方法通过http post机制，将表单内的各个字段与其内容放置在http header内一起传送至action属性所指向的URL地址，用户看不到这个过程。**

## 输入标记

### HTML4.01输入标记

\<input>是一个**单标记，且是行内标记必须嵌套在表**单标记中使用，用于定义一个用户的输入项。

````html
<form>
    <input name="" type="">
</form>
````

#### type类型属性值详解

- 单行文本输入框，text。

  表示该输入项的输入信息是字符串。此时，浏览器会在相应的位置会显示一个文本框。

  ````html 
  <form>
      <input name="a" type="text" maxlength="20" value="gg">
  </form>
  ````

  **value指的是默认值，如果不填则不会i产生显示此值**。

  <img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201102092417945.png" alt="image-20201102092417945" style="zoom: 80%;" />

- password

  `````html
  <form>
      <input name="b" type="password" maxlength="20" size="10">
  </form>
  `````

  <img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201102092752014.png" alt="image-20201102092752014" style="zoom: 80%;" />

- 复选框CheckBox

  ````html
  <form>
   苹果：<input name="c" type="checkbox" value="apple" checked>          <!-- checked表示默认选中-->
  </form>
  ````

  ![image-20201102093129120](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201102093129120.png)

- 单选框radio

  ````html
  <form>
   性别：<input name="d" type="radio" value="man" checked> 男
             <input name="d" type="radio" value="woman" >  女          <!-- checked表示默认选中-->
  </form>
  ````

  ![image-20201102093625998](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201102093625998.png)

  **先要完成单选，name必须要相同。不同选项的value的值应该不同。**

- 文件选择输入框file

  ````html
  <form action="url" method="post" enctype="multipart/form-data">
      <input type="file" name="e">
  </form>
  ````

  ![image-20201102094741563](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201102094741563.png)

  使用此功能时form中method要选择post；enctype="multipart/form-data"这段话是来确定以这种方式上传。

- 隐藏框hidden

  1、隐藏域在页面中对于用户是不可见的，在表单中插入隐藏域的目的在于收集或发送信息，以利于被处理表单的程序所使用。浏览者点击发送按钮发送表单的时候，隐藏域的信息也被一起发送到服务器。
  2、有些时候我们要给用户信息，让他在提交表单时提交上来以确认身份，如：sessionkey,etc,当然这些东西也能用cookie实现，但使用隐藏域就简单的多了，而且不会有浏览器不支持，用户禁用cookie的烦恼。
  3、有些时候一个form里有多个提交按钮，怎样使程序能够分清到底用户是按哪一个按钮提交上来的呢?我们就可以写一个隐藏域，然后在每一个按钮处加上`onclick="document.form.command.value="xx""`，然后我们接到数据后先检查command的值就会知道用户是按哪个按钮提交上来的。
  4、有些时候一个网页中有多个form，我们知道多个form是不能同时提交的，但有时候form确实互相作用，我们就可以在form中添加隐藏域来使它们联系起来。
  5、JavaScript不支持全局变量，但有时我们必须用全局变量，我们就可以把值先存在隐藏域里，它的值就不会丢失了。
  6、还有个例子，比如按一个按钮弹出9四个小窗口，当点击其中的一个小窗口时其他三个自动关闭．可是IE不支持小窗口相互调用，所以只有在父窗口写个隐藏域，当小窗口看到那个隐藏域的值是close时就自己关掉

- 提交按钮submit

  ````html
  <form>
      <input name="f" type="submit" value="提交" >          
  </form>
  value指的是按钮上面的字
  ````

  ![image-20201102101216223](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201102101216223.png)

- 图片按钮image

  ````html
  <form>
      <input name="g" type="image" src="url" >          
  </form>
  ````

  点击图片便可以提交。

- 重置按钮reset

  ````html
  <form>
      <input name="h" type="reset">          
  </form>
  产生一个重置按钮
  ````

  ![image-20201102101536852](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201102101536852.png)

  点击便可将本页面内容重新恢复到默认状态。

### HTML5新增输入标记

#### 新增标记选项

- 多行文本输入框（文本域）\<textarea>

  用\<textarea>标记一个超过一行的文本输入框，双标记，行内标记。

  `````html
  <textarea name="textarea" cols="40" rows="5" wrap>默认值</textarea>
  `````

  默认行有40个字符，列是5。wrap换行标记一般不写，窗口的默认值放在<></>之间。

- 下拉列表框

  在表单中，可以通过\<select>和\<option>标记可以在浏览器设计一个下拉式的带有滚动条的列表，用户可以在列表上选中一个或多个选项。

  ````html
  <form>
      <select name="friuts" size="1">
                  <option value="apple">苹果
                  <option value="banana" selected>香蕉
                  <option value="orange">橘子
      </select>
  </form>
  ````

  \<select>中有name和value属性；其中name是命名，size是指选框的行数，默认为1。

  \<option>中有value和selected两个属性；其中value是上传给服务器端的值，selected是指已经被选中的，选项值跟在标签后。\<option>也可以是双标记。

- 按钮标签

  \<button>标签定义一个按钮，双标记，之间是按钮上面的字体，也可以是图片啥的。其中type属性共有submit、reset、button三种。submit和reset的时候和input的相差无多，button时只是定义一个按钮。默认则是认为是一个提交按钮。

- label属性

  \<label>...\<label>在input元素定义标注lab**el标签中for属性，**应当与相关元素的ID相同。在单选或者复选框想要点击文字就选择到前面的框框，可以使用label标签。示例如下：

  ````html
  <form>
      <input type="radio" name="sex" ID="male"><label for="male">男</label>
      <input type="radio" name="sex" ID="female"><label for="female">女</label>
  </form>
  ````

  或者

  ````html 
  <form>
      <label> <input type="radio" name="sex">男 </label>
      <label><input type="radio" name="sex">女</label>
  </form>
  ````

  

- optgroup

  \<optgroup>标签把相关的选项组合在一起，来分组\<select>标记中的\<option>选项，其属性为label。

  ````html
  <form>
      <select name="city">
          <option selected disable>--请选择--</option>
          <optgroup label="河北省">
          <option value="SJZ">石家庄</option>
          <option value="QHD">秦皇岛</option>
          <option value="TS">唐山</option>
          <optgroup label="河南省">
          <option value="ZZ">郑州</option>
          <option value="LY">洛阳</option>
          <option value="KF">开封</option>
      </select>
  </form>
  ````

  optgroup既可以是单标记也可以是双标记，两者有些许的差别，单标记使用时好一些。其中label属性是给出分类方向，其值可以用汉字标出，只是做分类，不参与服务器数据交互。

  <img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201103103047164.png" alt="image-20201103103047164"  />

- \<datalist>属性

  - \<datalist>规定\<input>元素可能是选项的列表。在用来为\<input>元素提供自动生成的特性，用户能看到一个下拉列表，里面的选项是预先定义好的，将作为用户的输入。使用\<input>元素的list属性来绑定\<datalist>元素。

    ````html
    <form>
    搜索<input type="text" name="search" list="mylist">
    <datalist id="mylist">
        <option value="html教程"></option>
        <option value="html从入门到放弃"></option>
        <option value="css教程"></option>
        <option value="js教程"></option>
    </datalist>
    </form>
    ````

    ![image-20201103104726998](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201103104726998.png)
  

#### HTML5表单属性（了解）

- formaction：formaction="url"该属性会覆盖\<form>元素中的action属性。
- formenctype
- formmethod
- formtarget
- formnovalidate

#### HTML5新增form属性

- autocomplete：设置是否让浏览器有没有自动记录之前输入过的值，即历史记录。这个属性属于form标记的同时也属于input。默认是打开的。

  ````html 
  <form autocomplete="off|on">
      
  </form>
  ````

- novalidate：关闭表单提交时的自动验证。通常自动验证是关闭的，因为在不同浏览器中自动提示的内容是不同的，这是大家不想看的，通常会自己写。

#### HTML5新增input属性

- **placeholder：该提示会在输入字段为空时提示，并会在获得焦点前消失。**

  **适用于以下的\<input>类型：text、search、URL、telephone、email、以及password。**

- **autofocus：**自动获取焦点。

- **required：**用来验证表单项中是否为空，有空的就会提示同时也无法提交。

- **form**：使用form="ID"的方式将表单项指向相同的ID的form表单，并且一起提交。

- **multiple**：使用该属性允许用户输入选择多个组，使用的类型为type="file|email"，同时上传多个文件或者多个邮件地址，之间用“,”隔开。

- **pattern**：使用方法pattern="正则表达式"，如果不符合规则，会自动提示，并且不会提交。

  ````html
  <input type="tel" pattern="^(13|15|17)[0-9]{9}$">
  ````

  上面正则表达式中：^表示表达式开始，（）内表示前两位的数字用|区分，[]表示可允许输入的数字范围，{}表示还剩几位数，$结束符号。

#### HTML5新增input类型属性值

- date：日期，允许选择一个日期。
- **color：**进行颜色选择
- datetime：允许选择一个日期和时间（UTC时间），大部分浏览器不支持。
- datetime-local：允许用户选择一个时间和日期（不包含时区）。
- month：允许用户选择一个时间和月份。谷歌和edge支持，Firefox和IE不支持。
- time：允许选择一个时间。谷歌和edge支持，Firefox和IE不支持。
- week：允许选择年和第几周。谷歌和edge支持，Firefox和IE不支持。
- **email**：用于输入E-mail地址，并且提交表单时会自动验证。
- tel：与一般的文本框一样，没有自动验证的功能。
- number：控制用户输入数字的区间，可以设置最大值和最小值（包含max和min两个属性）。
- range：显示一个滑块，包括一定范围内的数字，进行选择，一般用于不需要很精确的选择，（属性包括min、max、value当前值、step移动一下的步数）。
- search：搜索域，显示的效果与text相同，最大的作业就是语义化。
- URL：输入一个网址，可以自动验证。
- button：创建一个按钮。

## 补充内容

### 只读和禁用

* readonly：只读，表单数据可以上传到服务器。
* disabled：禁用，表单数据不可以上传到服务器。

### name和ID的区别

- **id的用途**

1、id就是Client端HTML元素的Identity（标记），主要是在客户端脚本里用。
2、label与form控件的关联,如
 \<label for="MyInput">My Input\</label>
  \<input id="MyInput" type="text">
  for属性指定与label关联的元素的id，不可用name替代
3、脚本中获得对象：
IE支持在脚本中直接以id（而不是name）引用该id标识的对象。
例如上面的input，要在脚本中获得输入的内容，可以直接以 MyInput.value来获得。
如果用DOM的话，则用document.getElementById("MyInput").value，
如果要用name的话，通常先得到包含控件的form，例如document.forms[0]，然后从form再引用name，注意这样得到的是经过计算后将发送给服务器的值。

- **name的用途**

用途1: 主要是用于获取提交表单的某表单域信息， 作为可与服务器交互数据的HTML元素的服务器端的标示，比如input、select、textarea、框架元素(iframe、frame、 window的名字，用于在其他frame或window指定target)和button等，这些元素都与表单(框架元素作用于form的target)提交有关，浏览器会根据name来设定发送到服务器的request，在表单的接收页面只接收有name的元素, 所以赋ID的元素通过表单是接收不到值的。 我们可以在服务器端根据其Name通过Request.Params取得元素提交的值。在form里面，如果不指定Name，就不会发送到服务器端 。

用途2: HTML元素Input type='radio'分组，我们知道radio button控件在同一个分组类，check操作是mutex的，同一时间只能选中一个radio，这个分组就是根据相同的Name属性来实现的。

用途3: 建立页面中的锚点，我们知道<a href="URL">link</a>是获得一个页面超级链接，如果不用href属性，而改用Name，如：\<a name="PageBottom">\</a>，我们就获得了一个页面锚点。

用途4: 作为对象的Identity，如Applet、Object、Embed等元素。比如在Applet对象实例中，我们将使用其Name来引用该对象。

用途5: 在IMG元素和MAP元素之间关联的时候，如果要定义IMG的热点区域，需要使用其属性usemap，使usemap="#name"(被关联的MAP元素的Name)。
用途6: 某些特定元素的属性，如attribute，meta和param。例如为Object定义参数\<PARAM NAME = "appletParameter" VALUE = "value">或Meta中\<META NAME = "Author" CONTENT = "Dave Raggett">