# 第六讲 Symbol&Set和Map的数据结构

## Symbol

### 概述

ES5 的对象属性名都是字符串，这容易造成属性名的冲突。比如，你使用了一个他人提供的对象，但又想为这个对象添加新的方法（mixin 模式），新方法的名字就有可能与现有方法产生冲突。如果有一种机制，**保证每个属性的名字都是独一无二**的就好了，这样就从根本上防止属性名的冲突。这就是 ES6 引入`Symbol`的原因。**属于原始数据类型**。

````js
  var sn=Symbol('name')
    function person(){
        this[sn]='lily';
    }
    var p1=new person();
    var p2=p1[sn];
    console.log(p2); //lily
````

Symbol 作为属性名，遍历对象的时候，该属性不会出现在`for...in`、`for...of`循环中，也不会被`Object.keys()`、`Object.getOwnPropertyNames()`、`JSON.stringify()`返回。

但是，它也不是私有属性，有一个`Object.getOwnPropertySymbols()`方法，可以获取指定对象的所有 Symbol 属性名。该方法返回一个数组，成员是当前对象的所有用作属性名的 Symbol 值。

```javascript
const obj = {};
let a = Symbol('a');
let b = Symbol('b');

obj[a] = 'Hello';
obj[b] = 'World';

const objectSymbols = Object.getOwnPropertySymbols(obj);

objectSymbols
// [Symbol(a), Symbol(b)]
```

## Set数据结构

ES6 提供了新的数据结构 Set。它类似于数组，**但是成员的值都是唯一的**，没有重复的值。

`Set`本身是一个构造函数，用来生成 Set 数据结构。

```javascript
const s = new Set();

[2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x));//添加方法add()

for (let i of s) {
  console.log(i);
}
// 2 3 5 4
```

````js
    //ES6 提供了新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。
    let s=new Set([1,232,32,65,99,9,988,44,99,89,9,8,49,9]); //创建
    s.add('hello'); //添加
    s.add(9);  //重复的不添加
    s.add('9')  //不会转化
    // a.add({})   
    // s.add({});  //空对象可以重复添加
    console.log(s);
    let n=Array.from(s);
    console.log(n);
````

### 属性

- `Set.size`：返回`Set`实例的成员总数。

### 方法

- `Set.add(value)`：添加某个值，返回 Set 结构本身。
- `Set.delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
- `Set.has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
- `Set.clear()`：清除所有成员，没有返回值。

Set 结构的实例有四个遍历方法，可以用于遍历成员。由**于 Set 结构没有键名，只有键值（或者说键名和键值是同一个值），所以`keys`方法和`values`方法的行为完全一致**

- `Set.prototype.keys()`：返回键名的遍历器
- `Set.prototype.values()`：返回键值的遍历器
- `Set.prototype.entries()`：返回键值对的遍历器
- `Set.prototype.forEach()`：使用回调函数遍历每个成员

## Map数据结构

JavaScript 的对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。

```javascript
const map = new Map([
  ['name', '张三'],
  ['title', 'Author']
]);

map.size // 2
map.has('name') // true
map.get('name') // "张三"
map.has('title') // true
map.get('title') // "Author"
```