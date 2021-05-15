# 第二讲 环境的搭建

## 使用套件搭建

​	**基本不用了。**

手动引入几个库。

![mark](http://qiniu.wind-zhou.com/blog/210406/K1Hmke2id0.png?imageslim)

## 使用 create-react-app构建react开发环境

​	脚手架 搭建，一行命令即可。（第一次构建事件较长）

### （1）安装webpack-react-app

```js
npm install -g create-react-app
```

### （2）使用该命令创建项目目录

```js
create-react-app my-app
```

**注：不能包含大写字母**

### （3）切换到项目目录

```js
cd my-app
```

###  （4）运行项目

```js
npm start
```

运行后自动打开浏览器，默认运行在3000端口

## 手动搭建

### （1）首先搭建webpack环境

**此处不再列出。**，大家自行查阅。

### （2）安装项目依赖

 【1】安装loader

```js
$ cnpm install  @babel/preset-react  babel-loader @babel/core @babel/preset-env -D
```

 【2】安装react相关模块

 ```js
 cnpm  install react react-dom -D
 ```

 【3】手动配置webpack.config.js文件

```js
module: {
        rules: [
            	{
            test: /\.m?js$/,
            exclude: /(node_modules|bower_components)/,
            use: {
                loader: 'babel-loader',
                options: {
                    presets: ['@babel/preset-env', '@babel/react']
                }
            }
        }
      ]
    }
```



>注释：babel的作用不仅可以将es6转换为es5，还能将jsx转换为js文件，因此需要下载babel-loader

