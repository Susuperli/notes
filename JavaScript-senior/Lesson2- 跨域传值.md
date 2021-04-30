# 第二讲 跨域传值

## 同源策略

是一种约定，是浏览器最核心也是最基本的安全功能，如果缺少同源策略，浏览器的正常功能就会受到影响，现在支持JavaScript的浏览器都使用同源策略。

### 同源

所谓同源是指，域名、协议、端口号都相同。

## 跨域传值的方法

### Jsonp跨域

只支持get方法，不只post方法。

#### 原理

由于同源策略的限制，ajax只允许请求当前源（域名、协议、端口号）。

**利用src属性可以跨域传值的的特点，用户可以传递一个callback参数给服务器，然后服务器会返回数据时，会将这个callback参数作为函数来包裹住json数据。这样客户端就可以随意定制自己的函数来自动处理数据。**

``````js
<script>
    function test(data){
          处理函数;
}
</script>
<script src="http://localhost:80/web65/checkdata.php?callback=test"></script>
``````

#### jQuery中的jsonp

````js
$.aiax({
    url:"data.php?data=123",
    dataType:"jsonp",
    jsonp:"callback",  //传递给请求处理程序或页面的，用以获得jsonp回调函数名的参数名(一般默认为：callback，函数名会自动创建)
    //jsonpCallback:getdata,   //jquery在处理jsonp类型的ajax时自动帮你生成回调函数并把数据取出来供success舒心方法来调用，所以不用单独指定回调函数。
    success:function(data){
        for(var i in data){
            alert(i+","+data[i]);
        }
    }
})
````

### 跨域资源共享(CORS)

- CORS是一个W3C标准，全称是"跨域资源共享"(Cross-origin resource sharing)。它允许浏览器想跨源(协议+域名+端口号)服务器发出XMLHttpRequestrian请求，从而克服了ajax只能同源使用的限制。
- CORS需要浏览器和服务器同时支持。他的通信过程，都是浏览器自动完成，不需要用户参与。对于开发者来说，cors通信与同源ajax通信没有差别，代码完全一样。浏览器一旦发现ajax请求跨源，就会自动添加一些附加的头信息，有时还会多出一次附加的请求，但用户不会有感觉。
- 因此，实现从cors通信的关键是服务器。只要服务器实现了cors接口，就可以跨源通信。

#### 简单请求

对于简单请求，浏览器直接发出cors请求。具体来说，就是在头信息中，增加一个origin字段。

````cors
GET/cors HTTPS/1.1
Origin:http://api.bob.com  
Host:api.alice.com
Accept-Language:en-US
Connection:keep-alive
User-Agent:Mozilla/5.0...
````

上面的头信息中，Orgin字段用来说明，本次请求来自哪个源（协议+域名+端口）。服务器根据这个值，决定是否同意这次请求。

- Access-Control-Allow-Origin

  这个字段是必须的，他的值要么是请求Origin字段的值，要么是一个*，表示接受任意域名的请求。

- Access-Control-Allow-Credentials

  可选，表示是否允许发送cookie

- Access-Control-Expose-Headers

  可选。

#### 非简单请求

非简单请求的cors，会在正式通信之前，增加一次http查询请求，称之为“预检”请求。当前网页所在的域名是否在服务器的许可名单之中,以及可以使用哪些HTTP动词和头信息字段。只有得到肯定答复,浏览器才会为出正式的XMLHttpRequest请求,否则就报。

#### 与jsonp相比

- cors与jsonp的使用目的相同，但是比jsonp更强大。
- jsonp只支持GET请求，cors支持所有类型的http请求，jsonp的优势在于支持老式浏览器，以及可以向不支持cors的网站请求数据。

### window.name+iframe

![mark](http://qiniu.cloud-zhi.com/blog/210430/0kh56j34Jg.png?imageslim)

### postMessage() (html5 API)

### WebSocket (html5 API)

### 代理

