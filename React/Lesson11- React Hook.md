# 第十一讲 React Hook

## 简介

- hook是react 16.8版本增加的新特性/新语法
- 可以让你在函数组件中使用state以及其他的react特性

## 基本用法

### State Hook :React.useState()

- 让函数组件也可以有state状态，并进行状态数据的读写操作

- 语法：const [xxx,setXxx] = React.useState(initValue)

- useState()说明：

     参数：第一次初始化指定的值在内部做缓存，之后不再重新赋值。

     返回值：包含2个元素的数组。第一个为内部的当前状态值，第2个为更新的状态值的函数

- setXxx两种写法

  setXxx(newVlue)：参数为非函数，直接指定新的状态值，内部用其覆盖原来的状态值

  setXxx(value => newValue)：参数为函数，接收原来的状态值，返回新的状态值，内部用其覆盖原来的状态值

  ````React
  function Demo() {
      const [count,setCount]=React.useState(0)  //数组,设置状态，分别对应状态和更新状态的方法
      const [name,setName]=React.useState('tom')
      function add(){
          // setCount(count+1) //第一种写法
          setCount(count => count+1)  //第二种写法
      }
      function changeName(){
          setName('lily')
      }
      return (<div>
          <h2>当前求和是：{count}</h2>
          <h2>我叫：{name}</h2>
          <button onClick={add}>点我+1</button>
          <button onClick={changeName}>点我改名</button>
      </div>)
  }
  ````

### Effect Hook :React.useEffect()

- 可以让你函数组件中执行副作用操作（用于模拟类组件中的生命周期钩子）

- react中副作用操作

  - 发送ajax请求数据
  - 设置订阅/启动定时器
  - 手动更改真实DOM

- 语法说明

  `````react
  useEffect(() => {
      //任何副作用操作；
      return () => {  //组件卸载前执行，相当于componentWillUmmount()
          //在此做一些收尾工作，比如清除定时器
      }
  },[stateValue])   //如果是[],回调函数在第一次render()后执行相当于componentDidMOunt()；数组里面的参数可以时时刻刻监听一个变量，此时相当于componentWillUpdata()
  `````

- 可以吧useEffect Hook可以看成三个函数的组合

  - componentDidMOunt()
  - componentWillUpdata()
  - componentWillUmmount()

  `````react
  function Demo() {
      const [count,setCount]=React.useState(0)  //数组,设置状态，分别对应状态和更新状态的方法
  
      React.useEffect(() => {
          let timer=setInterval(() => {
              setCount(count+1)
          },1000)
          return () =>{
              clearInterval(timer)
          }
      },[])
      function add(){
          // setCount(count+1) //第一种写法
          setCount(count => count+1)  //第二种写法
      }
      function unMount(){
          ReactDom.unMountComponentAtNode(document.getElementById('root'))
      }
      return (<div>
          <h2>当前求和是：{count}</h2>
          <button onClick={add}>点我+1</button>
          <button onClick={unMount}>点我卸载</button>
      </div>)
  }
  `````

### Ref Hook :React.useRef()

- 可以在函数组件中存储，查找组件内的标签或者任意其他数据

- 语法：const refContainer = useRef()

- 作用：保存标签对象，功能和React.createRef()一样

  `````react
  function Demo() {
  
      const myRef = React.useRef()
  
      function show(){
          alert(myRef.current.value)
      }
  
      return (<div>
          <input type="text" ref={myRef}/>
          <button onClick={show}>点我提示数据</button>
      </div>)
  }
  `````

  

