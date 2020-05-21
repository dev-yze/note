#### 一、Generator函数

##### 1、基本概念

- 什么是Generator函数
  - ES6提供的一种异步编程解决方案
  - Generator函数可以理解为一个状态机，里面封装了多种状态
  - 执行Generator函数会返回一个遍历器对象，Generator除了状态机，还是一个遍历器对象生成函数。返回的遍历器对象，可以依次遍历Generator函数内部的每一个状态
  
- 特征

  ```
  function * demo() {
      yield 'hello';
      yield 'world';
      return 'ending';
  }
  let demoP = demo();
  ```

  - `function`关键字和函数名之间有个`*`
  - 函数体使用关键字`yield`表达式定义不同的状态
  - 调用函数与普通函数相同，但返回的不是执行结果，而是一个指向内部状态的指针对象，也就是遍历器对象

##### 2、`yield`命令

- 定义函数内部状态，只有通过调用next方法才会遍历下一个内部状态
- 遇到yield表达式就暂停后面的操作，并紧跟在`yield`后面的哪个表达式的值会作为返回对象的value值
- `yield`表达式只能在Generator函数里面用

##### 3、`next`方法

- `yield`表达式本身没有返回值或者返回undefined，next()方法可以带一个参数，该参数就会被当作上一个yield表达式的值
- 调用next返回一个具有value和done属性的对象，调用next方法运行到yield时done为false，运行到return表达式时，done为true

##### 4、throw方法和return方法

##### 5、generator函数与for...of循环

##### 6、yield*表达式

##### 7、作为对象属性的generator函数

##### 8、的



#### 二、用法

