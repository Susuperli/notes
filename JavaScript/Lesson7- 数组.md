#  第七讲 数组

## 数组的概念

**数组**（Array）是有序的元素序列。若将有限个类型相同的变量的[集合](https://baike.baidu.com/item/集合/2908117)命名，那么这个名称为数组名。组成数组的各个变量称为数组的分量，也称为数组的元素，有时也称为[下标变量](https://baike.baidu.com/item/下标变量/12713827)。用于区分数组的各个元素的数字编号称为下标。数组是在[程序设计](https://baike.baidu.com/item/程序设计/223952)中，为了处理方便， 把具有相同类型的若干元素按有序的形式组织起来的一种形式。这些有序排列的同类数据元素的集合称为数组

## 数组的创建

- 直接创建

  ````js
  var 数组名=[元素1,元素2,元素3,......];
  ````

  数组最简便的创建方法。

- 指定数组元素

  ````js
  var 数组名=new Array(元素1,元素2,元素3,.....);
  ````

  也可以是空数组

  ````js
  var 数组名=new Array()
  ````

- 指定数组长度

  ````js
  var 数组名=new Array(size);
  ````

  举例如下

  ````js
  	//创建
  	var arr=[10,"hi",true];//创建方法，简便方法。
  	var arr1=new Array();//创建方法，实例化，比较正统的方法。空数组，符合规则。运行速度慢。
  	var arr2=new Array("张三","李四","小明");
  
  	var arr3=new Array(5);//长度为5的数组，最小为5，最长不限。与2相比速度更快。
  	
  ````

## 数组的使用

### 输出和赋值

````js
       //输出
	document.write(arr2);//输出数组
	document.write(arr[0]);//输出数组arr中第0个元素。称为索引或是下标。
	//赋值
	arr1[0]="你好";//数组的赋值，只能通过索引的方法。
	arr1[5]="hello";//数组的赋值，只能通过索引的方法。
	document.write(arr1);
	
````

输出就可以直接输出。赋值可以在初始化时直接给出，后面赋值的时候只能单个赋值。

### 数组的遍历

`````js
       //数组里面所有元算都乘以2
       arr[0]=arr[0]*2;
	arr[1]=arr[1]*2;
	arr[2]=arr[2]*2;
	arr[3]=arr[3]*2;
	arr[4]=arr[4]*2;
	arr[5]=arr[5]*2;//直接更改
`````

````js
for(var i=0;i<arr.length;i++){
		arr[i]=arr[i]*2;
	}//循环更改
````

注：arr.length;表示数组的长度。

## 数组排序

### 冒泡排序

```js
for(var j=0;j<arr.length-1;j++){//控制循环次数。
		for(var i=0;i<arr.length-1-j;i++){//一轮之后，最大的数析出，在最后放出现，后续的比价不需要比较最后一位，循环的可以省略一步。
			if(arr[i]>arr[i+1]){//如果前比后大，前后交换位置，最小的向前。
				var a=arr[i];
				arr[i]=arr[i+1];
				arr[i+1]=a;
			}
		}
	} 
	document.write(arr)
```

### 选择排序

````js
for(var i=0;i<arr.length-1;i++){
		for(var j=i+1;j<arr.length;j++){//一轮之后，最小的数析出，放在最前面，后续的比较不需要比较。
			if(arr[i]>arr[j]){
				var a=arr[i];
				arr[i]=arr[j];
				arr[j]=a;
			}
		}
	}//选择排序

	document.write(arr);
````

### sort()排序

`````js
//sort()排序
	var newarr=arr.sort(function(a,b){return a-b;})//a-b降序，b-a升序
	document.write(newarr)
`````

## 数组的方法和属性

### 属性

arr.length：数组的长度。

### 方法

- 添加元素

  底部添加元素：**数组名.push(元素1,元素2,.....)**。//区别字符串和数值型变量，字符串需要添加""。

  头部添加元素：**数组名.unshift(元素1,元素2,...)**。

  ````js
  var arr=["浪","可","xue","省"];
  arr.unshift("j",1,1.333,"+");
  document.write(arr);
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/glGbjA5mDG.png?imageslim)

- 删除元素

  delete 数组[index];  用得少。

  ```js
  var arr=["浪","可","xue","省"];
  delete arr[1];
  document.write(arr);
  ```

  删除数组的最后一个元素

  `````js
  arr.pop();
  `````

  删除数组的顶部元素

  ````js
  arr.shift();
  ````

- 查询数组中是否有指定元素

  indexOf();如果有指定元素，将返回索引值（如果有多个的话，只输出第一个的索引值。），否则将会返回-1。

  使用该语句可以来去重。如下：

  `````js
  var arr=[1,2,3,3,56,655,8989,45,3,1,3,1,4];
     var newarr=[];//定义新的数组来储存新的没有重复的数组
     for(var i in arr){//数组的遍历
     if(newarr.indexOf(arr[i])==-1){//如果新数组里面没有原数组中的元素，触发条件，写入新的数组。
         newarr.push(arr[i]);
       }
      }
     alert(newarr)
  `````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/bC2LLG3i7k.png?imageslim)

  

- 颠倒顺序

  reverse();**用于颠倒数组中元素的顺序。该方法只是会改变原来的数组，但是不会创建新的数组**。

- **sort();**方法的排序

  参考博客：https://www.cnblogs.com/saifei/p/9043821.html

  sort()  方法用于对数组的元素进行排序，并返回数组。默认排序顺序是根据字符串UniCode码。因为排序是按照字符串UniCode码的顺序进行排序的，所以首先应该把数组元素都转化成字符串（如有必要），以便进行比较。

  语法：arrayObject.sort(sortby);

  参数sortby  可选，用来规定排序的顺序，**但必须是函数**。

  如果要得到自己想要的结果，不管是升序还是降序，就需要提供比较函数了。该函数比较两个值的大小，然后返回一个用于说明这两个值的相对顺序的数字。

  比较函数应该具有两个参数 a 和 b，其返回值如下：

  **若 a 小于 b，即 a - b 小于零，则返回一个小于零的值，数组将按照升序排列。**

  **若 a 等于 b，则返回 0。**

  **若 a 大于 b, 即 a - b 大于零，则返回一个大于零的值，数组将按照降序排列。**

  ````js
  //sort()排序
  	var newarr=arr.sort(function(a,b){return a-b;})//a-b降序，b-a升序
  	document.write(newarr)
  ````

- 合并数组

  使用数组对象的concat方法就可以将多个数组的元素链接到一起，生成一个新的数组，顺序按添加的顺序。

  var newarr=arr.concat(arr1,arr2,...);

  ````js
  var a=[1,2,3],b=[4,5,6];
  var c=a.concat(b);
  console.log(c);// 1,2,3,4,5,6
  console.log(a);// 1,2,3  不改变本身
  document.write(arr);
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/aLkJm7H1fE.png?imageslim)

  该方法需要新建新的数组来接受连接后的元素。**只是生成新的数组，不会改变原来的数组。**

- 字符转换(**将数组转化为字符串**)

  toString();将数组中的各个元素按照顺序排列成字符串返回。原数组并不会改变，生成新的数组变成了字符串，元素也变成了字符。

  数组名.toScring();

  ````js
  var arr = new Array(3)
          arr[0] ="北京";
          arr[1] = "上海";
          arr[2] = "广州";
  		var newarr=arr.toString()
  		document.write(arr);
  		document.write("<br>");
  		document.write(newarr);
  		document.write("<br>");
                document.write(typeof arr);
  		document.write("<br>");
  		document.write(typeof newarr);
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/8LKJLk391H.png?imageslim)

- 字符连接

  arr.join(分隔符)；使用join方法可以将数组按照要求的分隔符分开的样式，同时也会将各元素组成字符串返回。

  默认是“,”，如果想使用空格可以使用""空引号来表示空格。

  ````js
  var arr = new Array(3)
  arr[0] = "George"
  arr[1] = "John"
  arr[2] = "Thomas"
  
  document.write(arr.join("#"))
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/mfcEJkKLcm.png?imageslim)

- 更新移动数据

  - splice方法

    splice() 方法向/从数组中添加/删除项目，然后返回被更改的项目。

    数组名.splice(删除位置的下标(准确的说在下标位置前),删除的个数(可以是0，表示增添元素),插入元素1,插入元素2,...)。当只有一个数字时，表示从此处开始包括本身，删除后面的值。**splice方法会改变原来数组。**

    例子 1

    在本例中，我**们将创建一个新数组，并向其添加一个元素**：

    ```js
    <script type="text/javascript">
    
    var arr = new Array(6)
    arr[0] = "George";
    arr[1] = "John";
    arr[2] = "Thomas";
    arr[3] = "James";
    arr[4] = "Adrew";
    arr[5] = "Martin";
    
    document.write(arr + "<br />");
    arr.splice(2,0,"William");//只是在此处添加了一个新的元素并无删减
    document.write(arr + "<br />");
    
    </script>
    ```

    输出：

    ![mark](http://qiniu.cloud-zhi.com/blog/210430/ablhl6dGg5.png?imageslim)

    例子 2

    在本例中我们将删除位于 index 2 的元素，并添加一个新元素来替代被删除的元素：

    ```js
    <script type="text/javascript">
    
    var arr = new Array(6)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    arr[3] = "James"
    arr[4] = "Adrew"
    arr[5] = "Martin"
    
    document.write(arr + "<br />")
    arr.splice(2,1,"William")
    document.write(arr)
    
    </script>
    ```

    输出：

    ![mark](http://qiniu.cloud-zhi.com/blog/210430/d8206K2Ehb.png?imageslim)

    例子 3

    在本例中我们将删除从 index 2 ("Thomas") 开始的三个元素，并添加一个新元素 ("William") 来替代被删除的元素：

    ```js
    <script type="text/javascript">
    
    var arr = new Array(6)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    arr[3] = "James"
    arr[4] = "Adrew"
    arr[5] = "Martin"
    
    document.write(arr + "<br />")
    arr.splice(2,3,"William")
    document.write(arr)
    
    </script>
    ```

    输出：

    ![mark](http://qiniu.cloud-zhi.com/blog/210430/9iIEbcIjc5.png?imageslim)

  - slice

    定义和用法

    slice() 方法可从已有的数组中返回选定的元素。

    语法

    ```js
    arrayObject.slice(start,end)
    ```

    | 参数  | 描述                                                         |
    | :---- | :----------------------------------------------------------- |
    | start | 必需。规定从何处开始选取。如果是负数，那么它规定从数组尾部开始算起的位置。也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。 |
    | end   | 可选。规定从何处结束选取。该参数是数组片断结束处的数组下标。如果没有指定该参数，那么切分的数组包含从 start 到数组结束的所有元素，**不包含这个数**。如果这个参数是负数，那么它规定的是从数组尾部开始算起的元素。 |

    返回值

    返回一个新的数组，包含从 start 到 end （**不包括该元素**）的 arrayObject 中的元素。

    说明

    请注意，**该方法并不会修改数组**，而是返回一个子数组。如果想删除数组中的一段元素，应该使用方法 Array.splice()。

    提示和注释

    **注释：**可以使用负值从数组的尾部选取元素。

    **注释：**如果 end 未被规定，那么 slice() 方法会选取从 start 到数组结尾的所有元素。

    实例

    例子 1

    在本例中，我们将创建一个新数组，然后显示从其中选取的元素：

    ```js
    <script type="text/javascript">
    
    var arr = new Array(3)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    
    document.write(arr + "<br />")
    document.write(arr.slice(1) + "<br />")
    document.write(arr)
    
    </script>
    ```

    输出：

    ![mark](http://qiniu.cloud-zhi.com/blog/210430/bajG689D36.png?imageslim)**

    例子 2

    在本例中，我们将创建一个新数组，然后显示从其中选取的元素：

    ```js
    <script type="text/javascript">
    
    var arr = new Array(6)
    arr[0] = "George"
    arr[1] = "John"
    arr[2] = "Thomas"
    arr[3] = "James"
    arr[4] = "Adrew"
    arr[5] = "Martin"
    
    document.write(arr + "<br />")
    document.write(arr.slice(2,4) + "<br />")
    document.write(arr)
    
    </script>
    ```

    输出：

    ![mark](http://qiniu.cloud-zhi.com/blog/210430/JGEmmhhC40.png?imageslim)

- forEach();方法

  forEach() 方法用于调用数组的每个元素，并将元素传递给**回调函数**。括号里面要用函数表示。**该方法会改变原来的数组而不是生成新的数组。**对数组进行遍历循环，对数组中的每一项进行给定函数，这个方法没有返回值，参数都是function类型，默认有传参，参数分别为：遍历的数组内容，对象的数组的数值索引数据本身。

  **注意:** forEach() 对于空数组是不会执行回调函数的。

  ````js
  var arry=[1,44,22,88,54]
  array.forEach(
      function(currentValue, index, arr){//arr选填，可以省略。value指的是数组中存储的数据，index则是对应的索引值。
      
  })
  ````

  ````js
  //forEach():方法
  var arr=[2,56,45,1,23,7,79,5]
  var newarr=arr.forEach(function sum(zhi,index){
  	if(zhi%2==0){
  		arr[index]*=2;
  	}
  })
  document.write(arr)//该方法会改变原来的数组
  ````

- map();方法

  指的映射，对于数组中的每一项运行给定函数，返回每次函数调用的结果组成一个数组。**经常用来遍历数组。**

  map() 方法**返回一个新数组**，方法的参数是函数，数组中的元素为原始数组元素调用函数处理后的值。函数的参数分别是，value当前值即数组中的值，index索引值，arr数组。**产生一个新的数组不会改变原来的数组。**

  map() 方法按照原始数组元素顺序依次处理元素。

  **注意：** map() 不会对空数组进行检测。

  **注意：** map() 不会改变原始数组。

  ```js
  var array=[1,2,4,6,54,265,3]
  array.map(function(currentValue,index,arr){
      
  })
  ```

  ````js
  var arr=[2,56,45,1,23,7,79,5];
  var newarr=arr.map(function sum(value,index,arr){
  	return value=value*2
  })
  document.write(newarr)
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/5aCD20gEJE.png?imageslim)

- filter();方法

  过滤功能，数组中的每一项运行给定的函数好，返回值满足过滤条件组成的数组。

  filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

  **注意：** filter() 不会对空数组进行检测。

  **注意：** filter() 不会改变原始数组。

  `````js
  array.filter(function(currentValue,index,arr), thisValue)
  `````

  ````js
  var arr=[2,56,45,1,23,7,79,5];
  var newarr=arr.filter(function sum(value,index,arr){
  	return value>30;
  })
  document.write(newarr);
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/He0bhEajgK.png?imageslim)

  和map方法的区别

  ````js
  var arr=[2,56,45,1,23,7,79,5];
  var newarr=arr.filter(function sum(value,index,arr){
  	return value>30;
  })
  document.write(newarr);
  ````

  ![mark](http://qiniu.cloud-zhi.com/blog/210430/7a4aH4GcJK.png?imageslim)

  返回值是布尔型。

  

