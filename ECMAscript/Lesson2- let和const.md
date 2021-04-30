# 第二讲 let和const

## let命令

新增了let命令，用来声明变量。用法类似var，但是所声明的变量，只在let命令所在的代码块中有效。

- for循环还有特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的自自作用域。

  ````js
      var list=document.getElementById("list").children;
      for(let i=0;i<list.length;i++){
          list[i].onclick=function(){
              console.log(i)
          }
      }
  ````

- 不存在变量提升

  ````js
   alert(x); //undefined  变量提升
      var x=10;
  ````

  ````js
  lert(x); //保存 不支持变量提升
      let x=10;
  ````

- 暂时性死区

  ````js
    x=10;
      {
          alert(x);  //报错，暂时性死区
          let x=5;
      }
      alert(x)
  ````

## const

- 声明一个只读的常量。一旦声明便不能更改。
- 声明时必须赋值，否则报错。
- 不能重复声明。
- 不能提升常量，同样存在暂时性死区。

## 解构赋值

### 基本用法

es6允许按照一定的模式，从数组和对象中提取值，对变量进行赋值，这被称为解构

`````js
 let [x, y, z] = ["lily", ["tom", "张三"], "jerry"];//x,y,z在这里不是数组
    console.log(x,y,z);
`````

![解构](D:\0-Link\naotes\ECMAscript\picture\解构.png)

![image-20210326204826217](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210326204826217.png)

### 对象的解构赋值

与数组不同的是，数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

````js
let {foo,bar}={foo:"sss",bar:"sv"};
console.log(bar)
````

![image-20210326205845530](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210326205845530.png)

![image-20210326205853328](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210326205853328.png)

### 用途

- 交换变量的值

  ````js
  let x=1,y=2;
  [x,y]=[y,x]
  ````

- 从函数返回到多个值

- 函数参数的定义

  解构赋值可以方便地将一组参数与变量名对应起来

- 提取json数据

  ````js
  let jsonData={
      id:42,
      status:'ok',
      data:[5656,656]
  }
  let {id,status,data:number}=jsonData
  ````

  

