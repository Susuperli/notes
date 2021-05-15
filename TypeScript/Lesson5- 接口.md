# 第五讲 接口 类

## 接口

接口是一系列抽象方法的声明，是一些方法特征的集合，这些方法都应该是抽象的，需要由具体的类去实现，然后第三方就可以通过这组抽象方法调用，让具体的类执行具体的方法。

TypeScript 接口定义如下：

```ts
interface interface_name { 
}
```

````ts
interface IPerson { 
    firstName:string, 
    lastName:string, 
    sayHi: ()=>string 
} 
 
var customer:IPerson = { 
    firstName:"Tom",
    lastName:"Hanks", 
    sayHi: ():string =>{return "Hi there"} 
} 
 
console.log("Customer 对象 ") 
console.log(customer.firstName) 
console.log(customer.lastName) 
console.log(customer.sayHi())  
 
var employee:IPerson = { 
    firstName:"Jim",
    lastName:"Blakes", 
    sayHi: ():string =>{return "Hello!!!"} 
} 
 
console.log("Employee  对象 ") 
console.log(employee.firstName) 
console.log(employee.lastName)
````

## 类

### 创建

TypeScript 是面向对象的 JavaScript。

类描述了所创建的对象共同的属性和方法。

TypeScript 支持面向对象的所有特性，比如 类、接口等。

TypeScript 类定义方式如下：

```
class class_name { 
    // 类作用域
}
```

定义类的关键字为 class，后面紧跟类名，类可以包含以下几个模块（类的数据成员）：

- **字段** − 字段是类里面声明的变量。字段表示对象的有关数据。
- **构造函数** − 类实例化时调用，可以为类的对象分配内存。
- **方法** − 方法为对象要执行的操作。

创建一个 Person 类：

`````ts
class Person { }
`````

编译以上代码，得到以下 JavaScript 代码：

````ts
var Person = /** @class */ (function () {    function Person() {    }    return Person; }());
````

### 继承

TypeScript 支持继承类，即我们可以在创建类的时候继承一个已存在的类，这个已存在的类称为父类，继承它的类称为子类。

类继承使用关键字 **extends**，子类除了不能继承父类的私有成员(方法和属性)和构造函数，其他的都可以继承。

TypeScript 一次只能继承一个类，不支持继承多个类，但 TypeScript 支持多重继承（A 继承 B，B 继承 C）。

语法格式如下：

```ts
class child_class_name extends parent_class_name
```

`````ts
class Shape { 
   Area:number 
   
   constructor(a:number) { 
      this.Area = a 
   } 
} 
 
class Circle extends Shape { 
   disp():void { 
      console.log("圆的面积:  "+this.Area) 
   } 
}
  
var obj = new Circle(223); 
obj.disp()
`````

### static关键字

static 关键字用于定义类的数据成员（属性和方法）为静态的，静态成员可以直接通过类名调用。

`````ts
class StaticMem {  
   static num:number; 
   
   static disp():void { 
      console.log("num 值为 "+ StaticMem.num) 
   } 
} 
 
StaticMem.num = 12     // 初始化静态变量
StaticMem.disp()       // 调用静态方法
`````

