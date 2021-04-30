# 第三讲 面向对象开发

## 对象

### 概念

万物皆对象

### 封装

把相关的信息（属性和方法）储存在对象中的能力，封装性是指讲对象相关的信息和行为状态捆绑成一个单元，即将对象封装为一个具体的类。封装隐藏了对象的具体体现，当要操纵对象时，只需调用其中的方法，而不用管方法的具体实现。

### 继承

由另一个类（或多个类）的来类的属性和方法的能力。

### 多态

编写能以多种方法运行的函数或方法的能力。

### 类和对象的关系

类是对象的抽象，而对象是类的具体事例。

## 模式

### 创建对象的方法

- 原始模式
- 工厂模式
- 构造函数模式
- 原型模式
- 混合模式
- 构造-原型模式

### 原始模式

使用Object构造函数创建或字面量表示法

````js
var 对象名=new Obeject();
对象.属性名=值；
对象.方法名=fu();
````

`````js
    var person=new Object();  //创建
    person.name="张三";  //定义属性
    person.age="20";
    person.sayName=function(){  //定义方法
        alert(person.name)
    }
    person.run=function(){
        alert("跑起来！")
    }
    person.sayName();
`````

### 工厂模式

通过创建一个包含对象细节的函数来创建对象，然后返回这个对象

`````js
function 函数名(形参1,形参2){
     var 对象名=new Object(){
      对象名.属性值=形参1;
         对象名.方法名=fn();
         return 对象名;
     }
}
`````

``````js
    function person(name,age){
        var ps=new Object();
        ps.name=name;
        ps.age=age;
        ps.sayName=function(){
            alert(ps.name)
        }
        return ps;
    }
    var ps1=person("张三",'40');
    var ps2=person('李四','20');
    console.log(ps1)
``````

弊端：并**没有解决**对象的识别问题，即怎么知道一个对象的类型。工厂模式**解决了**重复实例化多个对象的问题，但是没有解决对象的问题（工厂模式无从识别对象的类型，因为全部都是Object,不像Data、Array等）。

#### 检测对象类型

`````js
Object.prototype.toString.call();
obj  instanceof Array;   //检测是否为此种类型
obj.constrcutor
`````

### 构造函数模式

构造函数模式并不需要创建中间对象并且可以将构造函数的事例标识为一种特定的类型，构造函数使new操作符来创建实例。

`````js
function 函数名(参数1,参数2){
    this.属性名=参数1;
    this.属性名=参数2;
    this.方法名=fn();
}
var 对象名=new 函数名(实参1,实参2);
对象名.方法名();
`````

````js
    function Person(name, age) {  //函数名即为构建函数的类型。
        this.name = name;
        this.age = age;
        this.sayName = function () {
            alert(this.name)
        }
    }
    var p1 = new Person('lily', '20');  //构造函数的创建
    var p2=new Person('tom','30');

    // console.log(p1,p2);
    p1.sayName();
````

与工厂模式相比：

- 没有显式的创建对象
- 直接将属性和方法赋给了this对象，this指向该构造函数构造出来的对象。
- 没有return语句

缺点：每个方法都有在每个实例上重新创建一遍。两个对象都有的方法，但是两个方法不是同一个function实例。不同实例上的同名函数是不相等的。

如下解决方法：

````js
    function Person(name, age) {
        this.name = name;
        this.age = age;
        this.sayName = fn;
    }
    function sn(){
        alert(this.name);
    }
    var p1 = new Person('lily', '20');  //构造函数的创建
    var p2 = new Person('tom', '30');

    // console.log(p1,p2);
    p1.sayName();
````

把sayName属性设置成全局的sayName函数，这样，由于sayName包含的是同意指向函数的指针，因此共享一个函数。但是，如果对象需要定义很多方法，那么就要定义很多个全局函数，自定义的引入类型也没有封装可言。

### 原型模式

#### prototype

参考博客：https://www.jianshu.com/p/eff5e130fc28

我们创建的每个函数都会有prototype属性，这个属性是一个指针，指向该函数的原型对象对象，通过构造函数构造出来的对象都自动拥有构造函数的prototype指针指向的对象的属性和方法（共享的），**函数原型对象当中的所有方法和属性，都是不占用内存的**。并且prototype对象当中的**属性和方法都是可以修改**![mark](http://qiniu.cloud-zhi.com/blog/210430/5IkA0kKji8.png?imageslim)

#### prototype和\_\_proto\_\_的区别

- function是对象，function的原型prototype也是对象，他们都会具有对象共同的特点。即：对象具有属性\_\_proto\_\_，每个对象都会在其内部初始化一个属性，就是\_\_proto\_\_，当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么他就会去\_\_proto\_\_里找这个属性，这个\_\_proto\_\_又会有自己的\_\_proto\_\_，于是就这样一直找下去，也就是我们平时所说的**原型链**的概念。
- function这个特殊对象，除了有\_\_proto\_\_属性之外，还会有特有的属性，原型属性(prototpe)。原型对象也有一个属性，叫做constructor，这个睡醒包含一个指针，指回原构造函数。
- **proto是实例对象用来直接访问构造函数的属性，prototype是函数对象的原型属性。**

### 补充

#### this

- 在js中，this指针是在创建函数时，由系统默认生成的两个隐式参数（另一个是arguments参数对象）。
- this指针指向与该函数调用进行隐式关联的一个对象。

#### this指针指向

- 方法，表示这个对象调用某种方法。
- 函数，this绑定全局对象。
- 构造函数调用模式，用new调用this绑定在新对象上。
- **apply，call，用来改变this的指向对象。P1.sayName.apply.p2;**
- es6中this指向固定化，始终指向外部元素，因为箭头函数没有this。

#### new关键字

- 在没有实例化之前，就是new之前，它的属性，方法等等在内存中都是不存在的。只有new了以后，这个类的一些动关系在内存中才会真的存在。
- 在js中，通过new可以产生源对象的一个实例对象，而这个实例对象继承了源对象的属性和方法。因此，**new的存在的意义在于它实现了js中的继承**，而不仅仅是实例化了一个对象。

### 混合模式



## 继承

参考：https://segmentfault.com/a/1190000008739672

参考：https://segmentfault.com/a/1190000008754962

- 原始对象继承
- 构造继承
- 原型链继承
- 组合继承
- 寄生式继承
- 寄生组合继承

### 原始对象继承

通过new关键字继承js原生构造函数Object的属性方法

var obj=new Object()

### 原型链继承

核心：将父类的实例作为子类的原型

````js
function person(name,age){
   this.name=name;
    this.age=age;
}
person.prototype.say=function(){
    alert(this.name)
}


function student(g){
    this.grade=g;
}

student.prototype=new person("tom","21")//关键语句，将父类原型作为子类的原型。
student.prototype.intr=function(){
    alert(this.grade)
}
var stu=new student(5)
stu.say()  //输出为tom
````

#### 特点

- 非常纯粹的继承关系，实例是子类的实例，也是父类的实例。
- 父类新增原型方法/原型属性，子类都能访问到。
- 简单、易于实现。

#### 缺点

- 要想为子类新增属性和方法，必须要在new person()这样的语句之后执行，不能放到构造器中。
- 无法实现多继承。
- 来自原型对象的**引用属性**是有实例共享的。
- 创建子类实例时，无法向父类构造函数传参。

### 构造继承

核心：使用父类的构造函数来增强子类实例，等于是复制父类的实例给子类（没有用到原型）

````js
function ClassA(scolor){  //构造原型函数ClassA()
    this.color=scolor;
    this.sayColor=function(){
        alert(this.color)
    }
}


function ClassB(bcolor,bNname){
    this.newmethod=ClassA;
    this.newmethod(bcolor);//通过子类的实例对象来调用父类构造函数，改变其中this的指向，相当于使用call(),apply()方法。
    //ClassA.call(this,bcolor)
    delete this.newmethod;  //删除多余的newmethod
    this.name=bName;      //为B设置新的属性
    this.sayName=function(){  //为B设置新的方法
        alert(this.name)
    }
}

var b=new ClassB("red","lily")
console.log(b)
````

#### apply()方法和call()方法

##### 相同点

都是用来改变this的指向

##### 不同点

传参方法不同

````js
B.apply(A,[])  //B中的方法和属性转到A上，数组传参
````

````js
B.call(A,'')  //字符串传参
````

#### 特点

- 解决了原型链中，子类实例共享父类引用属性的问题
- 创建子类实例时，可以向父类传递参数
- 可以实现多继承（call多个父类对象）

#### 缺点

- 只能继承父类的实例属性和方法，不能继承原型属性&方法
- 无法实现函数复用，每个子类都有父类实例函数的副本，影响性能

### 组合继承

指的是将**原型链**和借用**构造函数**的技术组合到一起。

思路是使用原型链实现对原型方法的继承，而通过借用构造函数来实现对实例属性的继承。这样，即通过在原型上定义方法和实现了函数的复用，又能够保证每个实例都有自己的属性。

````js
    function A(name){   //构建父类函数
        this.name=name;  //定义父类属性
    }
    A.prototype.say=function(){  //定义父类函数的方法
        alert(this.name)
    }
    function B(number,name){ //构建子类函数
        
        //第二次调用父类函数
        A.call(this,name);  //使用构造函数的方法，使A中的this指向自子类函数
        this.num=number;    //添加子类独有的属性
    }

    //第一次调用父类函数
    B.prototype=new A();  //子类原型对象通过new继承父函数实例
    B.prototype.constructor=B; // 由于上一步的原因，prototype.constructor指向了A，这对我们后面可能会造成困扰，这里使它重新指向B
    var b=new B(10,'狗') //创建B的实例

    b.say();   //自身没有say()方法，通过原型链访问
    alert(b.num)  //自身添加的属性同样有效
````

#### 特点

- 弥补了构造继承的缺陷，可以继承实例属性方法，也可以继承原型属性方法。
- 既是子类的实例，也是父类的实例。
- 不存在引用属性共享问题。
- 可传参。
- 函数可复用。

#### 缺点

- 无论什么情况下，都会调用两次父类构造函数

### 寄生式继承

与构造函数和工厂模式类似，创建一个仅用于封装继承过程的函数，该函数在内部以某种方法来增强对象，最后返回对象

````js
    function createA(name) {
        //创建新对象
        var obj = Object.create(name);  //复制对象
        //增强功能
        obj.sayO = function () {
            console.log("from O")
        };
        //返回对象
        return obj;

    }
    var A = {
        name: 'A',
        color: ['red', 'green', 'blue']
    };
    //实现继承
    var B = createA(A);
    console.log(B)//Object {name: "A", color: Array[3]}
    B.sayO();//from O 
````

不能做到函数的复用，即不能继承原型函数的方法

#### Object()和Object.creat()的区别

Object.cerate() 必须接收一个对象参数，创建的新对象的原型指向接收的参数对象，new Object() 创建的新对象的原型指向的是 Object.prototype. （表述有点啰嗦，简洁点说就是前者继承指定对象， 后者继承内置对象Object）
可以通过Object.create(null) 创建一个干净的对象，也就是没有原型，而 new Object() 创建的对象是 Object的实例，原型永远指向Object.prototype.

### 寄生组合式继承

核心：通过寄生的方式，砍掉父类的实例属性，这样，在调用两次父类的构造的时候，就不会初始化两次实例方法/属性，避免了组合继承的缺点

`````js
    function animal(name){  //创建父类
        this.name=name
    }
    animal.prototype.showname=function(){ //添加原型对象方法
        alert(this.name);
    }
    function cat(number,name){  
        animal.call(this,name);  //组合继承，通过call改变this指向。
        this.num=number;   //添加新的方法
    }
    (function(){   //实现寄生继承
        var Super=function(){};   //创建空函数接收原型对象方法
        Super.prototype=animal.prototype;
        cat.prototype=new Super();
    })();
    cat.prototype.constructor=cat;  //修复cat.prototype.constructor的指向方向

    var cat=new cat(10,'狗');
    cat.showname();
    alert(cat.num)
`````

**new操作符具体干了什么**
1、创建一个空的对象 var obj=new Object（）；
2、让空对象的原型属性指向原型链，设置原型链 obj.proto=Func.prototype;
3、让构造函数的this指向obj，并执行函数体 var result=Func.call(obj);
4、判断返回类型，如果是值就返回这个obj，如果是引用类型，返回这个引用对象。

#### 特点

- 只调用了一次supertype构造函数，因此能避免在subtype.prototype上创建不必要的，多余的属性。与此同时，原型链还能保持不变，还能正常使用instanceof和isPrototypeOf(),因此，寄生组合式继承被认为是引用类型最理想的继承范式。

#### 缺点

- 实现较为复杂





