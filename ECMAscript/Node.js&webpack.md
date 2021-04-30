# Node.js&webpack

## webpack的配置文件

`````js
const path=require('path');
module.exports={
    mode:"development",  //配置打包文件
    entry:"./src/index.js", //入口文件
    output:{                 //出口文件
        path:path.resolve(__dirname,'dist'),//path必须是绝对路径
        filename:'main.js'
    }
}
`````

### js多入口

````js
const path=require('path');
module.exports={
    mode:"development",  //配置打包文件
    entry:["./src/index.js", "./src/index2.js"]//入口文件
    output:{                 //出口文件
        path:path.resolve(__dirname,'dist'),//path必须是绝对路径
        filename:'main.js' //名字随便起
    }
}
````

### 多入口多出口

`````js
const path=require('path');
module.exports={
    mode:"development",  //配置打包文件
    entry:{
        index:"./src/index.js", 
        index2:"./src/index.js"
     }//入口:文件
    output:{                 //出口文件
        path:path.resolve(__dirname,'dist'),//path必须是绝对路径
        filename:'[name]-main.js' //filename前面我们可以使用一个变量[name],这个就表示获取entry里面的key作为文件名加在前面
//打出来是index-bundle.js和index2-bundle.js
    }
}

`````

## loader

webpack本身只能处理JavaScript模块，如果要处理其他类型的文件，就需要使用loader进行转换。

### css

css-loader和style-loader

### 图片

loader之图片处理（要和file-loader一起使用）

