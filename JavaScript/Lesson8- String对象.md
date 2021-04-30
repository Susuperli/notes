# 第八讲 String对象

## string对象-字符串对象

### 概念

说明：凡是用""或是''包裹的元素都是字符串，表单文本框所有内容都是字符串。

### 创建方法

直接赋值型：var str="lily"，类型为string。

new string();构造函数创建，类型为object。

## 字符串的方法和属性

### 方法

length属性。

### 属性

需要注意的是，JavaScript 的字符串是不可变的（immutable），**String 类定义的方法都不能改变字符串的内容**。像 **String.toUpperCase() 这样的方法，返回的是全新的字符串，而不是修改原始字符串。**

- char At(index);返回指定位置的字符。

  ````js
  stringObject.charAt(index)
  ````

  其中index是指想要返回值的索引值，必填。

  ````js
  var str="Hello world!"
  document.write("The first character is: " + str.charAt(0) + "<br />")
  document.write("The second character is: " + str.charAt(1) + "<br />")
  document.write("The third character is: " + str.charAt(20))
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/f2b61iKGLJ.png?imageslim)

  **注释：**字符串中第一个字符的下标是 0。如果参数 index 不在 0 与 string.length 之间，该方法将返回一个空字符串。

- concat(string1,string2,.....)

  concat() 方法将把它的所有参数转换成字符串，然后按顺序连接到字符串 stringObject 的尾部，并返回连接后的字符串。**stringObject 本身并没有被更改**。stringObject.concat() 与 Array.concat() 很相似。

  ````js
  stringObject.concat(stringX,stringX,...,stringX);
  ````

  通常会使用"+"链接。

- formCharCode();从字符编码创造一个字符串。（用得少）。

  charCodeAt() 方法可返回指定位置的字符的 Unicode 编码。这个返回值是 0 - 65535 之间的整数。

  方法 charCodeAt() 与 charAt() 方法执行的操作相似，只不过前者返回的是位于指定位置的字符的编码，而后者返回的是字符子串。

  ````js
  stringObject.charCodeAt(index);
  ````

- indexOf()

  indexOf() 方法可返回某个指定的字符串值在字符串中**首次**出现的位置。

  ````js
  stringObject.indexOf(searchvalue,fromindex)
  ````

  其中value是要检索的值，可以是一个字符也可以是一个字符串；index是指起始位置，选填如果没有则认为是从头开始。如果有则会返回索引值，否则则返回-1，区分大小写。

  `````js
  var str="Hello world!"
  document.write(str.indexOf("Hello") + "<br />")
  document.write(str.indexOf("World") + "<br />")//其中W为大写
  document.write(str.indexOf("world"))
  `````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/kfc88lH0IK.png?imageslim)

- lastIndexOf(检索值[,开始检索值]);从后面检索。

  lastIndexOf() 方法可返回一个指定的字符串值**最后**出现的位置，在一个字符串中的指定位置从后向前搜索。

  与前中方法相似，只不过是从后面开始找。

  ````js
  var str="Hello world!"
  document.write(str.lastIndexOf("l") + "<br />")
  document.write(str.lastIndexOf("World") + "<br />")
  document.write(str.lastIndexOf("world"))
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/mmH81GBfJl.png?imageslim)

- slice(start,end)

  slice() 方法可提取字符串的某个部分，并以新的字符串返回被提取的部分。

  ````js
  stringObject.slice(start,end)
  ````

  其中，start是指要抽取的片断的起始下标。如果是负数，则该参数规定的是从字符串的尾部开始算起的位置。也就是说，-1 指字符串的最后一个字符，-2 指倒数第二个字符，以此类推；end是指紧接着要抽取的片段的结尾的下标。若**未指定此参数**，则要提取的子串包括 start 到原字符串结尾的字符串。如果该参数是负数，那么它规定的是从字符串的尾部开始算起的位置。String.slice() 与 Array.slice() 相似。**不会改变原来的字符串**。

  ````js
  var str="Hello happy world!"
  document.write(str.slice(6,11))
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/6Lgb3Jm9ic.png?imageslim)

- substr(start,length);截取字符串。

  substr() 方法可在字符串中抽取从 *start* 下标开始的指定数目的字符。

  ````js
  stringObject.substr(start,length)
  ````

  其中，start为必需是指要抽取的子串的起始下标。必须是数值。如果是负数，那么该参数声明从字符串的尾部开始算起的位置。也就是说，-1 指字符串中最后一个字符，-2 指倒数第二个字符，以此类推；length为可选，子串中的字符数。必须是数值。如果省略了该参数，那么返回从 *stringObject* 的开始位置到结尾的字串。

  **注释：**substr() 的参数指定的是子串的开始位置和长度，因此它可以替代 substring() 和 slice() 来使用。

  **重要事项：**ECMAscript 没有对该方法进行标准化，因此反对使用它。

  ````js
  var str="Hello world!"
  document.write(str.substr(3))
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/58gL288gc0.png?imageslim)

- substring(start,stop)

  和slice方法相似，不同点为该方法不能取负。substring() 方法用于提取字符串中介于两个指定下标之间的字符。

  `````js
  stringObject.substring(start,stop)
  `````

  其中，start为必需是指一个非负的整数，规定要提取的子串的第一个字符在 stringObject 中的位置；stop为可选。一个非负的整数，比要提取的子串的最后一个字符在 stringObject 中的位置多 1，即**不包括stop本身**。如果省略该参数，那么返回的子串会一直到字符串的结尾。

  ````js
  var str="Hello world!"
  
  document.write(str.substring(3))
  document.write("<br>")
  document.write(str.slice(3))
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/dLh5lAEebh.png?imageslim)

- split()

  split() 方法用于**把一个字符串分割成字符串数组**。与Array.join();所执行的效果相反，是将（）内的内容变成分隔符，隔开。

  `````js
  stringObject.split(separator,howmany)
  `````

  其中，separator是指分隔符的地方，必需，字符串或正则表达式，从该参数指定的地方分割 stringObject。**howmany为可选，该参数可指定返回的数组的最大长度**。如果设置了该参数，**返回的子串不会多于这个参数指定的数组**。如果没有设置该参数，整个字符串都会被分割，不考虑它的长度。

  ````js
  var str="How are you doing today?"
  
  document.write(str.split(" ") + "<br />")//在空格处进行分割。
  document.write(str.split("") + "<br />")//空字符，表示每个字母都进行分割。
  document.write(str.split(" ",3))//空格处分割，且超过三个字母的字符串不予显示。
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/DEjg87L8m5.png?imageslim)

  - 老师给的小例子

    ````js
    	   //老师举的小例子
            var website="http://www.qhdlink.com?name=lily&pwd=1234&age=18";
    		
    		var qs=website.slice(website.indexOf("?")+1);//name=lily&pwd=1234&age=18
    		var qarr=qs.split("&");//name=lily,pwd=1234,age=18
    		var qsvalue=[];
    		for(var i=0;i<qarr.length;i++){
    			var sarr=qarr[i].split("=");//字符串的索引值
    			qsvalue.push(sarr[1]);//被=分割后分成前后两个字符串，索引值为0，1将需要的输入定义的空数组
    		}
    		
    		console.log(typeof qarr);
    		document.write(qarr+"<br>");
    		document.write(qsvalue);
    ````

- toLowerCase(),将字符串转化为小写。

- toUpperCase(),将字符串转化为大写。

