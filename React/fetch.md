# fetch

多年来，XMLHttpRequest一直是web开发者的亲密助手。无论是直接的，还是间接的，当我们谈及Ajax技术的时候，通常意思就是基于XMLHtpRequest的Ajax，它是一种能够有效改进页面通信的技术。Ajax的兴起是由于Google的Gmail所带动的，随后被广泛的应用到众多的Web产品(应用)中，可以认为，开发者已经默认将XMLHttpRequest作为了当前Web应用与远程资源进行通信的基础。而以下介绍的内容则是XMLHttpRequest的最新替代技术——Fetch APIl，它是W3C的正式标准。![mark](http://qiniu.cloud-zhi.com/blog/210421/L9I515H9kl.png?imageslim)

`````React
class Fetch extends React.Component{
    state={data1:''}
    render(){
        let data=Object.values(this.state.data1);
        return(<div>
            {data.map(function(value){
            return(<div key={value.id_coach}>{value.name_coach} <span> {value.type_coach}</span></div>)
        })}
        </div>)
    }
    componentDidMount(){
        let req=new Request('http://www.qhdlink-student.top/student/coacha.php',{
            method:'post',
            headers:{'content-type':'application/x-www-form-urlencoded'},
            body:'username=zyp&userpwd=123456&userclass=64&type=4'
        })
        fetch(req).then(function(response){
            return response.json()
        }).then((data)=>{
            console.log(data)
            this.setState({data1:data})
        })
    }
}
`````

## 简单使用

![mark](http://qiniu.cloud-zhi.com/blog/210421/jiIIEe030i.png?imageslim)

### 强制带Cookie

默认情况下，fetch不会从服务端发送或者接收任何cookie，如果站点依赖于维护一个用户会话，则导致未经认证的请求（要发送cookie，必须发送凭据头）

`````js
fetch('url',{
    methof:'GET',
    credentials:'include', //强制加入凭据头
}).then((res)=>{
    return res.text()
}).then((res)=>{
    console.log(res)
})
`````

## 数据交互

### 添加

### 删除

### 更改

### 查询





