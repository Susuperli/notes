# 第九讲 Math&Date&Number&Error对象

## Math对象

### 属性

- E 属性：返回自然对数的底数e。
- LN10：返回10的自然对数。
- LN2：返回2的自然对数。
- LOG2E：返回以2为底，e的对数。
- LOG10E：返回以10为底，e的对数。
- PI：返回π。
- SQPT1_2：返回2的平方根的倒数。
- SQRT2：返回2的平方根。

### 方法

- **floor(x)：对数进行下舍入。**
- **ceil()：对数进行上舍入。**
- **round(x)：把数四舍五入为最为接近的整数**。
- log(x)：返回数的自然对数（底为e）。
- **max(x,y)：返回x和y中的最大值。**
- **min(x,y)：返回x和y的最小值。**
- pow(x,y)：返回x的y次幂。
- **random：随机生成0~1之间的随机数。**
- sin(x)：返回数的正弦。
- sqrt(x)：返回数的平方根。
- tan(x)：返回数的正切。
- valueOf()：返回Math对象的原始值。

**老师给的验证码的小例子**

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
	<i id="clikk"></i>
	<i onclick="yam()">点我一下</i>
</body>
<script type="text/javascript">
	var arr=["0","1","2","3","4","5","6","7","8","9","a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","w","v","x","y","z"]
	function yam(){
		var str="";//每次函数开始前都定义一个新的字符串。
		for(var i=0;i<5;i++){
			var num=Math.floor(Math.random()*36);//随机生成0~35的数字。
			str+=arr[num];//关键语句，写入str，因为每次都会生成一个随机数，累加生成验证码。
		}
		document.getElementById("clikk").innerHTML=str;
	}
	yam();
</script>
</html>
````



![mark](http://qiniu.cloud-zhi.com/blog/210430/lk2JdKfl5f.png?imageslim)

## Date对象

### 创建Date

new Date();构建函数创建Data对象。

### 属性

prototype属性

### 方法

#### get方法

- getDate()：从date对象返回同一个月中的某一天（1~31）。
- getDay()：从date对象中返回一周的某一天（0~6），0是周日。
- getMonth()：从date对象返回月份返回月份（0~11）。
- getFullYear()：从date对象返回四位数的年份。
- getHours()：从date对象返回小时（0~23）。
- getMinutes()：从date对象返回分钟（0~59）。
- getSeconds()：从date对象返回秒（0~59）。
- getMilliseconds()：从date对象返回毫秒（0~999）。
- getTime()：返回1970年1月1日至今的毫秒数，时间戳。
- parse()：返回1970年1月1日午夜到指定日期（字符串）的毫秒数。

#### set方法

- setDate()：设置从date对象同一个月中的某一天（1~31）。
- setDay()：设置从date对象中一周的某一天（0~6），0是周日。
- setMonth()：设置从date对象月份返回月份（0~11）。
- setFullYear()：设置从date对象四位数的年份。
- setHours()：设置从date对象小时（0~23）。
- setMinutes()：设置从date对象分钟（0~59）。
- setSeconds()：设置从date对象秒（0~59）。
- setMilliseconds()：设置从date对象毫秒（0~999）。
- setTime()：设置1970年1月1日至今的毫秒数，时间戳。

**老师给的计时器的小例子**

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
	<div id="time"></div>
</body>
<script type="text/javascript">
	function time(){
		var date=new Date();
		var hours=date.getHours();
		var minutes=date.getMinutes();
		var seconds=date.getSeconds();
		var ms=date.getMilliseconds();
		document.getElementById("time").innerHTML=hours+":"+minutes+":"+seconds+":"+ms;
	}
	setInterval(time,1000)
</script>
</html>
````

![mark](http://qiniu.cloud-zhi.com/blog/210430/253lk3IfCA.png?imageslim)

#### 转换

- toString()：转换为字符串。
- toDateString()：toString() 把 Date 对象转换为字符串。
- toTimeString() 把 Date 对象的时间部分转换为字符串。
- toDateString() 把 Date 对象的日期部分转换为字符串。
- toGMTString() 请使用 toUTCString() 方法代替。
- toUTCString() 根据世界时，把 Date 对象转换为字符串。
- toLocaleString() 根据本地时间格式，把 Date 对象转换为字符串。
- toLocaleTimeString() 根据本地时间格式，把 Date 对象的时间部分转换为字符串。
- toLocaleDateString() 根据本地时间格式，把 Date 对象的日期部分转换为字符串。
- UTC() 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。
- valueOf() 返回 Date 对象的原始值。

## Number对象

### 属性

- MAX_VALUE：可表示最大的值。
- MIN_VALUE：可表示最小的值。
- NaN：非数字值。
- NEGATIVE_INFINITY：负无穷大，溢出时返回该值。
- POSITIVE_INFINITY：正无穷大，溢出时返回该值。
- prototype：向对象添加属性和方法。

### 方法

没啥方法

## Erorr对象

### 概述

每当程序运行发生错误或是执行异常，用户可以调用erorr构造函数，就会创建erorr对象，erorr对象存储错误。

````js
var err=new Erorr();
````

### 属性

没啥

### 方法

没啥



