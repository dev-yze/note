1、同步回调和异步回调

同步回调: 调用函数中不存在异步方法，在调用函数按顺序执行回调函数，同步回调是阻塞的

异步回调：我们不希望在某个方法上一直阻塞，需要先执行后续的方法，那就是异步回调，调用一个方法，如果执行时间比较长，我们可以传入一个回调的方法，当方法执行完后，让被调用者执行给定的回调方法

2、异步编程方法

1) async和await



1) Generator函数

- 基本概念

  generator函数是ES6提供的一种异步编程解决方案,可以理解为一个状态机，里面封装了多种内部状态

  ```javascript
  function * demo() {
      yield 'hello';
      yield 'world';
      return 'ending';
  }
  let demoP = demo();
  ```

  特征:

  1. function关键字和函数名之间有个*，位置随意
  2. 函数体内部使用yield表达式，定义不同状态,上面有三个状态
  3. 函数调用通过next方法，每次调用next方法指针就从函数内部或上次停下来的地方开始执行，直到遇到下一个yield表达式或return为止,yield是暂停执行的标记，next方法可以恢复执行
  4. 调用next方法返回一个包含两个属性value和done的对象，value是yield表达式的值，done表示是否遇到return,遍历是否结束，结束done为true,未结束为false

- yield表达式

- next方法的参数

  `yield`表达式本身没有返回值，或者说总是返回`undefined`。`next`方法可以带一个参数，该参数就会被当作上一个`yield`表达式的返回值。

  ```javascript
  // next参数
  function* g1() { 
      for (let i = 0; true; i++) {
          let reset = yield i;
          console.log('reset的值为:' + reset);
          if (reset) {
              i = -1;
          }
      }
  }
  let g1r = g1();
  console.log(g1r.next());
  console.log(g1r.next());
  console.log(g1r.next());
  console.log(g1r.next());
  console.log(g1r.next());
  console.log(g1r.next(true));
  // 结果
  { value: 0, done: false }
  reset的值为:undefined
  { value: 1, done: false }
  reset的值为:undefined
  { value: 2, done: false }
  reset的值为:undefined
  { value: 3, done: false }
  reset的值为:undefined
  { value: 4, done: false }
  reset的值为:true //传进去的参数true被当作上衣yield表达式的值即reset=true
  { value: 0, done: false }
  ```

  

- next方法的参数



- ddd
- ddd
- ddd







