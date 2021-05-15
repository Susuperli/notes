# 第一讲 React简介

## 简介

- 9、React是用于构建用户界面的JavaScript框架
- 是一个将数据渲染为HTML视图的开源JavaScript库（主要是操作dom呈现）

### 特点

- 声名式设计 -React采用声名范式，可以轻松描述应用。
- **高效**- 使用虚拟DOM+diff算法，尽量减少与真实DOM的交互。
- 灵活 -React可以与已知的库或框架很好的配合。
- JSX -JSX是JavaScript语法扩展。React开发者不一定使用jsx但是推荐。
- **组件** -通过react构建组件，使得代码更加容易得到复用，能够很好的应用到大项目的开发中。
- **单向响应的数据流** -react实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更加简单。
- 在react native中可以使用react语法进行移动端开发。

## 模块化和组件化

### 模块化

简单来说，**模块化**就是将一个大文件拆分成相互依赖的小文件，再进行统一的拼装和加载。

### 组件化

模块化只是对文件层面上，对代码或是资源的拆分；而组件化是在设计层面上的，对ui的拆分。   

从UI上面拆分下来的包含模板（HTML）+样式（css）+逻辑（js）功能完备，我们称之为组件。

## 高效的性能

react实现的原理：virtual DOM

传统的web应用，操作DOM一般是直接更新操作的，但是我们知道DOM更新通常是比较昂贵的。而React为了尽可能减少对DOM的操作，提供了一种不同的而又强大的方式来更新DOM，代替直接的DOM操作。就是Virtual DOM,一个轻量级的虚拟的DOM，就是React抽象出来的一个对象，描述dom应该什么样子的，应该如何呈现。通过这个Virtual DOM去;更新真实的DOM，由这个Virtual DOM管理真实DOM的更新。

### diff算法

计算出Virtual DOM真正变化的部分，并只针对该部分进行原生DOM操作，而非重新渲染整个页面。

#### React的diff算法

将virtual dom转换成actual dom树的最少操作的过程称之为调和。diff算法是调和的具体实现。

#### diff策略

策略一tree diff

web UI中dom节点跨层级的移动操作特别少，可以忽略不计。

策略二component diff

拥有相同类的两个组件，生成相似的树状结构。

拥有不同类的两个组件，生成不同的树状结构。

策略三element diff

对于同一层级的一组节点，通过唯一id区分。

![mark](http://qiniu.cloud-zhi.com/blog/210421/cDIg16aH11.png?imageslim)

### 分离框架的设计

Reactjs现在的版本已经将源码分开为ReactDOM和React.js 这就意味着React不仅仅能够在web端工作，甚至还可以在服务端，native端进行。

与此同时，我们可以自定义自己的渲染器，实现比如Threejis, Pixijs, D3.js的React方式渲染。

## 应用范围

web端应用

原生应用 -iOS、Android、native应用

node.js服务端渲染html。