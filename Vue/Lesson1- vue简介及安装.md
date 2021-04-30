# 第一讲 vue简介及安装

## 简介

Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与[现代化的工具链](https://cn.vuejs.org/v2/guide/single-file-components.html)以及各种[支持类库](https://github.com/vuejs/awesome-vue#libraries--plugins)结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

vue.js的**目标**是通过尽可能简单的API实现响应的数据绑定和组合的视图组件

- 解决了数据绑定问题
- vue框架产生的目的的主要目的是为了开发大型单页应用
- 它还支持组件化，也就是可以将页面封装为若干个组件，采用积木式进行编程，这样是页面复用性达到最高（支持组件化）

### 和其他框架的区别

如果你已经是有经验的前端开发者，想知道 Vue 与其它库/框架有哪些区别，请查看[对比其它框架](https://cn.vuejs.org/v2/guide/comparison.html)。

### vue的特点

- **MVVM模式**Model-View-ViewModel（数据变量model发生改变视图发生变化，视图改变，数据变量也发生变化）

  - view和viewmodel之间采用双向绑定：view的变动，自动反应在viewmodel。反之亦然。

  - view与model不发生联系，都是通过viewmodel传递。

  - view非常薄，不部署任何业务逻辑，称为被动视图，即没有任何主动性，而viewmodel非常厚，所有逻辑都部署（指令，事件，dom监听）在在哪里。

  - model层主要是为应用程序提供数据，主要包括web services，reset services

- **组件化**

  在大型的应用中，为了分工、复用和可维护性，我们不可避免地需要将应用抽象为多个相对独立额模块。在较为多个相对独立的模块。在较为传统的开发模式中，我们只考虑复用时才会将某一部分作成为组价；但实际中，应用类UI完全可以看做是全部由组件构成的。

  因此，在vue.js的设计中将组件作为一个核心概念。可以说，每一个vue.js应用都是围绕组件来开发的。

  ![image-20210421115425744](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210421115425744.png)

- **指令系统**

  在vue.js中指令带有前缀v-，以表示他们是vue.js提供的特殊属性。他们会在渲染过程中DOM上应用特殊的响应式行为。

  