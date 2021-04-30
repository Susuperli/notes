# 第十一讲 Class类

## 基本写法

创建类

```javascript
class Point {   //class声明类型
  constructor(x, y) {  //添加属性
    this.x = x;
    this.y = y;
  }

  toString() {  //添加方法
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

继承

````javascript
    class Student extends Person{
        constructor(name,age,number){
            super(name,age);  //使用super()来继承
            this.num=number;  //添加新的方法
        }
    }
    let s=new Student("lily","18","123456");  //new 出新对象
    
    s.sayName();
````

