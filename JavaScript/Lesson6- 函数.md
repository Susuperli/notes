# 第六讲 函数

参考博客：https://blog.csdn.net/qq_34569497/article/details/95379260

## 自定义函数

函数是完成指定功能的程序段，可以反复调用，减少代码冗余。

### 创建自定义函数

`````javascript
function 函数名(形参1,形参2,....){
    语句;
    语句;
    ........;
    return 表达式/值；
}
`````

`````js
	function test(){
				var x=10;
				var y=20;
				var z=x+y;
				fn();
				alert(z);
			}
`````

### 调用函数

函数名(实参,实参,......)

说明：如果没有调用，函数则不会执行。

- 当事件发生时（当用户点击按钮时）
- 当 JavaScript 代码调用时
- 自动的（自调用）

### 有参函数

````js
 function sum(a,b){
			 var x=a;
			 var y=b;
			 var sum=x+y;
			 alert(sum)
		 }
````

### 带返回值的函数

1. **所有函数都会有函数返回值即函数执行后一定会返回一个结果，如果没有定义默认返回undefined**；
2. 在函数中，return后定义返回值；
3. 在函数中，return之后的代码就不会再执行了
4. return只能用于函数中，用在其他地方会报错。

参考博客：https://blog.csdn.net/weixin_45797022/article/details/104973715

```js
 function sum(x,y){
	var z=x+y;
	return z;    //在一个函数中只出现一次，只返回一个值，遇到return函数结束，写在最后一行。
	}
	var num=sum(3,5);    //必须有返回值才可以控制，如果没有返回值，输出undefined。
	 document.write(num);
	
```

### 匿名函数的使用

匿名函数，**可以将函数赋值到变量中var func = function(){};在其调用时需要用括号标识出。**

举例如下：

````js
//2，函数表达式：把函数存到变量或数组等里，调用时通过变量进行调用
	var fn = function(){
	    console.log("函数表达式：将函数存到变量里");
        //验证作用，可以检查函数执行的情况，与alert类似，但是不会打断代码的执行，可以在控制台中观察到。
	};
	fn();//调用时需要写括号

//数组中的调用同样需要加()
	var arr = [];
	arr[0] = function(){
	     console.log("函数表达式：将函数存到数组的对应位置");//验证作用，可以检查函数执行的情况，与alert类似，但是不会打断代码的执行，可以在控制台中观察到。
	};
	arr[0]();//调用时需要写括号要写括号
````

- 绑定事件时，可以使用。

  ````js
  <!DOCTYPE html>
  <html lang="zh">
  <head>
  	<meta charset="UTF-8">
  	<meta name="viewport" content="width=device-width, initial-scale=1.0">
  	<meta http-equiv="X-UA-Compatible" content="ie=edge">
  	<title></title>
  </head>
  <body>
  	<button type="button" onclick="sum(10,3)">按钮</button>
  </body>
  <script type="text/javascript">
  		 function sum(a,b){
  			 var x=a;
  			 var y=b;
  			 var sum=x+y;
  			 alert(sum)
  		 }
  </script>
  </html>
  ````

  点击按钮即可调用函数。

- 自调用

  ````js
  (function (){
      console.log("一次性");
  })();
  ````
  

参见博客：https://www.cnblogs.com/liushisaonian/p/9425427.html

### 回调函数

把一个函数作为另一个个函数的参数值传入，并且在该函数中调用，被传入的函数称为回调函数。

````js
  function test(x,callback){
  		var y=10;
  		var z=x+y;
  		callback(z);
  	}
  	test(50,function(c){alert(c)})
````

### 作用域

 全局变量：是指函数外的变量，可以在js的任意部分使用。

 私有变量：指的是函数内的变量，只能在本函数内使用。

  函数里面没有声明var，自动会变成全局变量。

  **区别：局部变量只能被其函数识别，因此可以在不同函数中使用相同名称的变量。**

  **局部变量在函数开始时创建，在函数完成时被删除。**

  ````js
  <!DOCTYPE html>
  <html>
      <body>
          <h2>JavaScript 函数</h2>
          <p>myFunction() 之外的 carName 未定义。</p>
          <p id="demo1"></p>
          <p id="demo2"></p>
      <script>
      myFunction(); //函数的调用
      function myFunction() {
          var carName = "Volvo";
          document.getElementById("demo1").innerHTML =
          typeof carName + " " + carName;
      }
      document.getElementById("demo2").innerHTML =
      typeof carName;//变量在此处失效类型为未定义
      </script>
      </body>
  </html>
  ````

![mark](http://qiniu.cloud-zhi.com/blog/210430/254A5Hmgla.png?imageslim)

## 系统（内置）函数

* URL编码函数：encodeURL()
* URL解码函数：decodeURL()
* 数据类型转换函数——转换为整型：parseInt();转换失败返回NaN。
* 数据类型转换函数——转换为浮点型：parseFloat();转换失败返回NaN。

