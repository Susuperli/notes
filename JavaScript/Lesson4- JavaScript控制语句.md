#  第四讲 JavaScript控制语句

## 结构

### 顺序结构

语句从上向下逐条进行，没有结构就是顺序结构。

### 单分支结构

单分支：要么做，要么不做。

````js
if(条件){
    语句1；
    语句2；
    .......；
}
````

说明：如果条件为true执行{}中的所有语句，否者跳过if（）外的结构。

### 双分支结构

要么做，否者做。

```js
if(条件){
 语句1；
 语句2；
  .......；
}else{
 语句；
}
```

说明：条件为true时执行所有语句，否则执行下面的语句。

````js
    var username=prompt("请输入用户名：");
    var password=prompt("请输入用户名：");
    if(username==1111&&password==1111){
        document.write("欢迎登陆!!!");
    }else{
        document.write("傻逼!!!");
    }
````

### 多分支结构

````js
if(条件){
    语句1；
    ........；
}else if(条件){
    语句1；
    ........；
}else if(条件){
    语句1；
    ........；
}else if(条件){
    语句1；
    ........；
}else{
    语句；
}
````

说明：由上而下顺序进行，条件成立时执行相应的条件，结构结束。

````js
var num=prompt("请输入分数：");
    if (num>=90) {
        document.write("A");
    }else if(num>=80) {
        document.write("B");
    }else if (num>=70){
        document.write("C");
    }
    else if (num>=60) {
        document.write("D");
    }
    else{
        document.write("F");
    }
````

### 多选一

```js
switch(表达式/变量){
    case 值1:
        语句1;
        ........;
        break;
    case 值2:
        语句1;
        ........;
        break;
    case 值3:
        语句1;
        ........;
        break;
    default:
        语句；
}
```

````js
switch(site){
        case "百度":
        location.href="https://www.baidu.com";
        break;
        case "网易":
        location.href="https://www.163.com";
        break;
        case "新浪":
        location.href="https://www.sina.com";
        break;
        default:document.write("只能访问百度、新浪、网易");
    }
````

## 循环

### for循环

````js
for(循环变量初始化;条件;增量){
    语句1;
    语句2;
    .........;
}
````

````js
  for(var i=1,u=0;i<=100;i++){
        if(i%2==0){
            u=u+i;
        }
        // else{
            
        // }
    }
    document.write(u)
````

九九乘法表

````js
 var mul,i=1,j=1;
    for(var i=1;i<10;i++){
        // if(i>=2){
        //     document.write("<br>")
        // }
        for(var j=1;j<=i;j++){
            mul=i*j;
            document.write(j+"X"+i+"="+mul+" ");
            if(j==i){
                document.write("<br>")
            }  
        }
    }
````

### while循环

直到型循环，直到条件为false时退出循环。

````js
var 循环变量初始化；
while(条件){
    语句；
    ........；
    增量；
}
````

````js
var sum=0,i=0;//初始化
	while(i<=100){//条件
		sum=sum+i;
		i++;//增量
	}
	document.write(sum)
````

### do-whlie循环

类似于while循环，但是该类型至少会执行一次。

````js
do{
    语句；
    ........；
    增量；
}while(条件);
````

### break&continue

- break：是指跳出循环。
- continue：结束本次循环，开始下一次循环。

