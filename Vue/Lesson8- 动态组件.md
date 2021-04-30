# 第八讲 动态组件&异步组件

## 动态组件

`````vue
<component v-bind:is="currentTabComponent"></component>
`````

父组件

`````vue
    <button @click='changeComponent("Mimi")'>点我显示1</button><button @click='changeComponent("Mini")'>点我显示2</button>
    <component :is="compons"></component>
`````

````jsx
      data:function(){
    return{
      compons:''
    }
changeComponent:function(data){
      this.compons=data;
    }
````

![mark](http://qiniu.cloud-zhi.com/blog/210423/BBiimbjbE5.wmv)

![mark](http://qiniu.cloud-zhi.com/blog/210423/E009ehC3h7.png?imageslim)

### keep-alive

**重新创建动态组件的行为通常是非常有用的，但是在这个案例中，我们更希望那些标签的组件实例能够被在它们第一次被创建的时候缓存下来。为了解决这个问题，我们可以用一个 `<keep-alive>` 元素将其动态组件包裹起来。**

`````vue
<!-- 失活的组件将会被缓存！-->
<keep-alive>
  <component v-bind:is="currentTabComponent"></component>
</keep-alive>
`````

## 异步组件（懒加载）

当使用[局部注册](https://cn.vuejs.org/v2/guide/components-registration.html#局部注册)的时候，你也可以直接提供一个返回 `Promise` 的函数：将不再import引入。

```jsx
new Vue({
  // ...
  components: {
    'my-component': () => import('./my-async-component')
  }
})
```

