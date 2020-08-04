1、vue的描述

- 构建用户界面的渐进式框架
- 被设计为自底向上逐层应用
- 只关注视图层

2、MVC和MVVM

MVC：后端开发概念

MVVM：前端页面视图层的分局开发思想，这里的M是保存在每个页面中的数据，VM是一个一个数据调用者，分割了M和V，每当V层想要获取数据时，通过VM做中间的处理，V就是每个页面中的HTML结构；V通过VM调用M中的数据，M通过VM将数据推送给V

3、vue应用

一个Vue应用由一个通过 `new Vue`创建的根实例，以及可选的嵌套的、可复用的组件树组成。

4、vue基础知识扫盲

- vue实例：构成vue应用的基础

  - 数据和方法

    - 响应式数据

      创建一个Vue实例时，会将data对象中的所有property加入到vue的响应式系统中，当property值发生改变，视图发生相应，即匹配更新为新的值

    - 注意

      - 只要当创建实例时就已经存在data中的property属性才是相应式的，新增加属性改变不会触发更新
      - 唯一例外是使用`Object.freeze()`会阻止修改现有的property，意味着系统无法追踪变化

  - 其它实例属性和方法(带有前缀$)

    ```javascript
    var data = { a: 1 }
    var vm = new Vue({
      el: '#example',
      data: data
    })
    vm.$el === document.getElementById('example') =>true
    vm.$data === data // => true
    vm.$watch('a', function (newValue, oldValue) {
      // 这个回调将在 `vm.a` 改变后调用
    })
    
    ```

    

  - 生命周期

    - 生命周期函数

    ​        vue实例在创建时要经过一系列的初始化过程，在这个过程中会运行一些叫做生命周期的函数，给用户在不同阶段添加代码，增加业务逻辑

    ​		生命周期函数顺序

    ​		beforeCreate()

    ​		created()

    ​		beforeMount()

    ​		mounted()

    ​		beforeDestroy()

    ​		destroyed()

    - 生命周期图片

      ![Vue 实例生命周期](https://cn.vuejs.org/images/lifecycle.png)

- 模板语法

  - 插值 

    - Mustache语法 {{}}
    - v-html
    - v-bind
    - javascrpt表达式(单个表达式)

  - 指令

    - 参数

    - 动态参数

      **从 2.6.0 开始，可以用方括号括起来的 JavaScript 表达式作为一个指令的参数：**

    - 修饰符

  - 缩写

- 计算属性和侦听

  - 计算属性和方法的区别

    计算属性是基于响应式依赖的，只有相关响应式依赖发生改变，才会重新求值

    方法每次调用都会重新求值

    对于那些基于响应式数据的值的变化的，使用计算属性会减小开销

  - 侦听属性

    观察和相应Vue实例上的数据变动

- Class与Style绑定

- 条件渲染

- 列表渲染

- 事件处理

- 表单输入绑定

- 组件