# 第六讲 条件渲染

## 条件渲染

React中的条件渲染和JavaScript中一样，使用JavaScript运算符if或者条件运算符来表现呢当前的状态，然后让React根据他们来更新UI。

### if结构

```React
if(!this.state.isLogin){
            return <div>
            <button onClick={this.login}>登录</button>
        </div>
        }
        else{
            return <div>欢迎登录</div>
        }
```

判断函数

`````React
 login=()=>{
        this.setState({'isLogin':!this.state.isLogin})
    }
`````

### &&符结构

````React
return <div>
            <button onClick={this.login}>登录</button>
            {this.state.isLogin && <div>hello world</div>}
        </div>
````

通过花括号包裹代码，你可以在JSX中嵌入任何表达式。这也包括JavaScript 中的逻辑与(&&)运算符。它可以很方便地进行元素的条件渲染。

如果条件是 true,&&右侧的元素就会被渲染，如果是false，React 会忽略并跳过它。

### 三目运算符

````React
return <div>
            {this.state.isLogin?<div onClick={this.login}>欢迎登录</div>:<div><button onClick={this.login}>登录</button></div>}
        </div>
````

## map()处理数组对象数据

遍历数组的方法

````React
 let datad=datat.map((value)=>{
            return <tr key={value.id_coach}><td>{value.id_coach}</td><td>{value.name_coach}</td><td>{value.type_coach}</td></tr>
        })
````

## key

- Keys可以在DOM中某些元素被增加或是被删除的时候帮助React识别哪些元素发生了变化。因此你应该给数组中的每一个元素赋予一个确定的标识。
- 一个元素的key最好是最各元素的在列表中拥有的一个独一无二的字符串。通常，我们使用来自数据的id作为元素的key当元素中没有确定的id时，你可以使用它的序列号索引index作为key（若元素没有重排，该方法还是不错的，但是发生重排后这个方法就会变慢）。

### 深度解析key的必要性

- key是React用于追诉那些列表中的元素被修改、被添加或者被移除的辅助性标志。
- 在开发过程中，我们需要保证某个元素的key在其同级元素中具有唯一性。在React Diff算法中React会借助元素的key值来判断钙元素是新晋创建的还是被移动而来的数据，从而减少不必要元素的重渲染。此外，React还需要借助key值来判断元素与本地状态的关联关，因此我们绝不可能忽视被转换函数中key的重要性。

