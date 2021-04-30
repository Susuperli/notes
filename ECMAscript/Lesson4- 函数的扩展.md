# 函数的扩展

## 函数参数的默认值

通常情况下，定义了默认值的参数，应该是函数的尾参数。因为这样比较容易看出来，到底省略了那些参数。如果非尾部的参数设置默认值，实际上这个参数是没法省略的。

`````js
    function test(x=5,y=10){
        alert(x+y)
    }
    test(undefined,2);
`````

### Rest参数

用于获取函数的多余的参数，rest参数搭配的变量是一个数组，该变量将多余的参数放入数组中

````js
   var 狗=11;
    function test(x,y,...z){ //...z接收所有剩余的参数，用数组的形式展示出。
        console.log(x);
        console.log(y);
        console.log(z);
    }
    test(1,12,122,122,545,45,8,7,45,58,8,1,54,87,4,4987,8,44,87,7,4,6489,77,87,97,987,9878,789,445,44,54,549884,5,"狗",狗)
````

### 严格模式

- 从es5开始，函数内部可以设定为严格模式。

- delete运算符后跟随非法标识符（delete不存在的标示符），会抛出语法错误；非严格模式下，会静默失败并返回false。

- 严格模式下，对象 直接量中电仪同名属性会抛出语法错误。

- 函数形参不能同名。

- 不允许八进制整数直接量。

- arguments对象是传入函数内参数列表的静态副本。

- eval和arguments当做关键字，他们不能被赋值和用做变量声明。

- 限制调用栈的检测能力，访问arguments，callee，caller会出错。

- 变量必须先声明。

- call，apply传入null或undefined保持原样不被转换为window。

  `````js
  function doSomething(a,b){
      'use strict';
      //code
  }
  `````


### name属性

````js
function foo(){
    
}
foo.name //"foo"
````

- 匿名函数中，es5使用该属性会返回空字符串，es6会返回被赋值的变量。

- function构造函数返回的函数实例，name属性的值为anonymous。

- bind返回的函数，name属性值会加上bound前缀。

  ````js
  function foo(){};
  foo.bind({}).name  //"bound foo"
  (function(){}.bind({})).name //"bound"
  ````

## 箭头函数

### 基本用法

````js
var f=v=>v;

//等同于
var f=function(){ return 5 };
````

如果不需要参数或多个参数，就是用一个圆括号代表参数部分。

`````js
var f=()=>5;
//等价于
var f=function(){ return 5 };


var sum=(num1,num2)=>num1 +num2;
//等同于
var sum=function(num1,num2){
    return num1+num2;
}
`````

如果箭头函数的代码多余一条语句，就要使用大括号将他们括起来

````js
var sum = (num1, num2) => { return num1 + num2; }
````

大括号被解释为代码块，所以如果箭头函数直接返回一个对象，必须在对象外面加上括号。

````js
// 报错
let getTempItem = id => { id: id, name: "Temp" };

// 不报错
let getTempItem = id => ({ id: id, name: "Temp" });
````

简化回调函数

```js
// 正常函数写法
[1,2,3].map(function (x) {
  return x * x;
});

// 箭头函数写法
[1,2,3].map(x => x * x);



// 正常函数写法
var result = values.sort(function (a, b) {
  return a - b;
});

// 箭头函数写法
var result = values.sort((a, b) => a - b);
```

结合rest参数

`````js
const numbers = (...nums) => nums;

numbers(1, 2, 3, 4, 5)
// [1,2,3,4,5]

const headAndTail = (head, ...tail) => [head, tail];

headAndTail(1, 2, 3, 4, 5)
// [1,[2,3,4,5]]
`````

### this指向问题

（1）函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。

（2）不可以当作构造函数，也就是说，不可以使用`new`命令，否则会抛出一个错误。

（3）不可以使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不可以使用`yield`命令，因此箭头函数不能用作 Generator 函数。

上面四点中，第一点尤其值得注意。`this`对象的指向是可变的，但是在箭头函数中，它是固定的。

````js
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

var id = 21;

foo.call({ id: 42 });
// id: 42
````

eg1:

````js
    var a=11
    function test1(){
      this.a=22;
      let b=function(){
        console.log(this.a);
      };
      b();
    }
    var x=new test1();
    //输出11
````

eg2:

`````js
    var a=11;
    function test2(){
    this.a=22;
    let b=()=>{console.log(this.a)}
    b();
    }
    var x=new test2();
     
    //输出22
`````

`this`指向的固定化，并不是因为箭头函数内部有绑定`this`的机制，实际原因是箭头函数根本没有自己的`this`，导致内部的`this`就是外层代码块的`this`。正是因为它没有`this`，所以也就不能用作构造函数。

## 方法的扩展

### Object.is()

ES5 比较两个值是否相等，只有两个运算符：相等运算符（`==`）和严格相等运算符（`===`）。它们都有缺点，前者会自动转换数据类型，后者的`NaN`不等于自身，以及`+0`等于`-0`。JavaScript 缺乏一种运算，在所有环境中，只要两个值是一样的，它们就应该相等。

ES6 提出“Same-value equality”（同值相等）算法，用来解决这个问题。`Object.is`就是部署这个算法的新方法。它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。

```javascript
Object.is('foo', 'foo')
// true
Object.is({}, {})
// false
```

不同之处只有两个：一是`+0`不等于`-0`，二是`NaN`等于自身。

```javascript
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

### Object.assign()

`Object.assign()`方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

```javascript
const target = { a: 1 };

const source1 = { b: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);  //改变了target的数组
target // {a:1, b:2, c:3}
```

其他类型的值（即数值、字符串和布尔值）不在首参数，也不会报错。但是，除了字符串会以数组形式，拷贝入目标对象，其他值都不会产生效果。

```javascript
const v1 = 'abc';
const v2 = true;
const v3 = 10;

const obj = Object.assign({}, v1, v2, v3); //用一个新的空对象接收。
console.log(obj); // { "0": "a", "1": "b", "2": "c" }
```

`````js
    let obj1={'name':'lily'};
    let obj2={'age':'20'};
    let obj3={'tel':'888888'};
    let obj=Object.assign({},obj1,obj2,obj3);  //同名属性后面的会把前面的覆盖掉。空对象不影响前面的对象。
    console.log(obj)
`````

`Object.assign()`拷贝的属性是有限制的，只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（`enumerable: false`）。

### 注意点 [§](https://es6.ruanyifeng.com/#docs/object-methods#注意点) [⇧](https://es6.ruanyifeng.com/#docs/object-methods)

**（1）浅拷贝**

`Object.assign()`方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。

```javascript
const obj1 = {a: {b: 1}};
const obj2 = Object.assign({}, obj1);

obj1.a.b = 2;
obj2.a.b // 2
```

上面代码中，源对象`obj1`的`a`属性的值是一个对象，`Object.assign()`拷贝得到的是这个对象的引用。这个对象的任何变化，都会反映到目标对象上面。

**（2）同名属性的替换**

对于这种嵌套的对象，一旦遇到同名属性，`Object.assign()`的处理方法是替换，而不是添加。

```javascript
const target = { a: { b: 'c', d: 'e' } }
const source = { a: { b: 'hello' } }
Object.assign(target, source)
// { a: { b: 'hello' } }
```

上面代码中，`target`对象的`a`属性被`source`对象的`a`属性整个替换掉了，而不会得到`{ a: { b: 'hello', d: 'e' } }`的结果。这通常不是开发者想要的，需要特别小心。

一些函数库提供`Object.assign()`的定制版本（比如 Lodash 的`_.defaultsDeep()`方法），可以得到深拷贝的合并。

**（3）数组的处理**

`Object.assign()`可以用来处理数组，但是会把数组视为对象。

```javascript
Object.assign([1, 2, 3], [4, 5])
// [4, 5, 3]
```

上面代码中，`Object.assign()`把数组视为属性名为 0、1、2 的对象，因此源数组的 0 号属性`4`覆盖了目标数组的 0 号属性`1`。

**（4）取值函数的处理**

`Object.assign()`只能进行值的复制，如果要复制的值是一个取值函数，那么将求值后再复制。

```javascript
const source = {
  get foo() { return 1 }
};
const target = {};

Object.assign(target, source)
// { foo: 1 }
```

上面代码中，`source`对象的`foo`属性是一个取值函数，`Object.assign()`不会复制这个取值函数，只会拿到值以后，将这个值复制过去。

### __proto__属性

`__proto__`属性（前后各两个下划线），用来读取或设置当前对象的原型对象（prototype）。目前，所有浏览器（包括 IE11）都部署了这个属性。

```javascript
// es5 的写法
const obj = {
  method: function() { ... }
};
obj.__proto__ = someOtherObj;

// es6 的写法
var obj = Object.create(someOtherObj);
obj.method = function() { ... };
```

该属性没有写入 ES6 的正文，而是写入了附录，原因是`__proto__`前后的双下划线，说明它本质上是一个内部属性，而不是一个正式的对外的 API，只是由于浏览器广泛支持，才被加入了 ES6。标准明确规定，只有浏览器必须部署这个属性，其他运行环境不一定需要部署，而且新的代码最好认为这个属性是不存在的。因此，无论从语义的角度，还是从兼容性的角度，都不要使用这个属性，而是使用下面的`Object.setPrototypeOf()`（写操作）、`Object.getPrototypeOf()`（读操作）、`Object.create()`（生成操作）代替。

```javascript
Object.getPrototypeOf(obj); //读取一个对象的原型
```

### Object.keys()

ES5 引入了`Object.keys`方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。

```javascript
var obj = { foo: 'bar', baz: 42 };
Object.keys(obj)
// ["foo", "baz"]
```

### Object.values() [§](https://es6.ruanyifeng.com/#docs/object-methods#Object-values) [⇧](https://es6.ruanyifeng.com/#docs/object-methods)

`Object.values`方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值。

```javascript
const obj = { foo: 'bar', baz: 42 };
Object.values(obj)
// ["bar", 42]
```

### Object.entries()

`Object.entries()`方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组。

```javascript
const obj = { foo: 'bar', baz: 42 };
Object.entries(obj)
// [ ["foo", "bar"], ["baz", 42] ]
```