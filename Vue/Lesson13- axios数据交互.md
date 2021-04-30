# 第十三讲 axios数据交互

Axios 是一个基于 promise 的 HTTP 库，可以用在浏览器和 node.js 中。

## 特性

- 从浏览器中创建 [XMLHttpRequests](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)
- 从 node.js 创建 [http](http://nodejs.org/api/http.html) 请求
- 支持 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API
- 拦截请求和响应
- 转换请求数据和响应数据
- 取消请求
- 自动转换 JSON 数据
- 客户端支持防御 [XSRF](http://en.wikipedia.org/wiki/Cross-site_request_forgery)

## 安装

使用 npm:

```jsx
$ npm install axios
```

`````jsx
import Axios from 'axios'
`````

````jsx
Vue.prototype.$axios=Axios
//调用时  this.$axios
````

`````jsx
// 发送 POST 请求
this.$axios({
  method: 'post',
  url: '/user/12345',
   header:{'Content-Type','application/x-www-form-urlendcoded'}
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});
`````

### 请求方法的别名

为方便起见，为所有支持的请求方法提供了别名

##### axios.request(config)

##### **axios.get(url[, config])**

##### axios.delete(url[, config])

##### axios.head(url[, config])

##### axios.options(url[, config])

##### **axios.post(url[, data[, config]])**

##### axios.put(url[, data[, config]])

##### axios.patch(url[, data[, config]])