字符串

正则



函数



对象



类



# JavaScript基础



## 字符串



### 方法



### 模板字符串

```javascript
let a = 5, b =1;
console.log(`a的值为${a},b的值为${b},a+b的值为${a+b}`); // a的值为5,b的值为1,a+b的值为6
```



## 数组

### 创建数组

- 数据直接量创建数组

  - 数据直接量中的值不一定要是常量，可以是任意的表达式，以及对象直接量或其它数组直接量
  - 省略数组中的某个值，省略的元素将被赋值为undefined
  - 数组直接量可以允许有可选的结尾的逗号，[,,]中只有两个元素

- 调用构造函数创建数组

  ```javascript
  var a = new Array();	// 无参数，等同于数组直接量[]
  var a = new Array(10);  // 有一个参数，指定数组的长度，预分配存储空间
  var a = new Array(4, 4, 2, 'test', 'testString');  // 显式指定两个或多个数组元素或者一个非数值元素，构造函数中的参数将成为新的数组元素
  ```

  

### 操作数组

```javascript
var a = ['world'];   // 从一个元素的数组开始
var value = a[0];    // 读取第0个元素
a[1] = 3.14;		// 写入第1个元素
let i = 2;
a[i] = 3;            // 写入第2个元素

let a = [];
a.length  // 数组的长度
```

```javascript
let a = [];

a['-123'] = 'm';
console.log('------------------a.length-------------------------');
console.log(a.length);   // 0
console.log(a['-123']);  // m
a['0.00'] = 0;    
console.log(a['0.00']);  // 0
console.log(a[0]);       // undefined
a[0.00] = 0;             
console.log(a[0]);       // 0
// 结果:

```

​	添加和删除数组元素：

- 为新索引赋值

- 使用push()方法在数组末尾增加一个或多个元素

- 使用unshift()方法在数组的首部插入一个元素

- 使用delete运算符来删除数组

  ```javascript
  let a = [1, 2, 3];
  delete a[1];   // a = [1, undefined, 3];
  console.log(a[1]);   // undefined
  console.log(a.length);	// 3
  ```

  

  - 删除类似于赋值undefined，不会改变数组的length()属性,不会将元素从高处索引移下填充已删除属性留下的空白

- 其它：pop()和push()、shift()和unshift()、splice()

- 使用for循环,可以根据需要从头部或者末尾进行遍历

```javascript
for (let i=0; i< a.length; i++) {}
for (let i= a.length - 1; i >= 0; i--) {}
for (let i=0, len = a.length; i < len; i++) {}  // 优化数组长度
```

- ​	跳过null、undefined和不存在的元素

  ```javascript
  for (let i = 0; i < a.lenght; i++) {
      if (a[i] === undefined) continue;   //跳过undefined和不存在元素
      if (!a[i]) continue;				// 跳过null、undefined和不存在元素
      if (!(i in a)) continue;			// 跳过不存在的元素
  }
  ```

- 使用for/in循环处理稀疏数组。循环每次将一个可枚举的属性名赋值给循环变量，不存在的索引将不会被遍历

  - 遍历属性不保证
  - for/in循环能枚举继承的属性，可通过检测过滤

```
for (let i in a) {
	if (!a.hasOwnProperty(i)) continue;  //跳过继承属性
	if (String(Math.floor(Math.abs(Number(i)))) !=== i) continue;  // 跳过不是负整数的i
}
```

- 使用forEach()方法进行函数式编程过滤

```
let data = [1, 3 , 5];
let sum = 0;
data.forEach(x => {
	sum += x;
});
```



### 稀疏数组和多维数组

​	稀疏数组：稀疏数组就是包含从0开始的不连续索引的数组。稀疏数组length属性值大于元素的个数

### `ECMA3`数组方法

#### (1) join()	

将数组元素转化为字符串连接在一起，返回最后生成的字符串,可指定连接符参数，默认逗号

#### (2) reverse()  

将数组中的元素颠倒排序，返回逆序数组

#### (3) sort()	

将数组中的元素排序并返回排序后的数组

#### (4) `concat`()

​	创建并返回一个新数组，它的元素包括调用concat()的原始数组的元素和concat()的每个参数，如果这些参数中任何一个自身是数组，则连接的是数组的元素。但concat()不会递归扁平化数组，concat()也不会修改调用的数组。

#### (5) slice()  

返回指定提取的数组片段

​	返回指定数组的一个片段或数组，它的参数分别指定了片段的开始和结束的位置，返回的数组包含第一个参数指定的位置和所有到但不含第二个参数指定的位置之间的数组元素，如果只指定一个元素，返回数组包含从开始位置到数组结尾的所有元素，如参数中出现负数，它表示相对于数组中最后一个元素的位置，如-1指定了最后一个元素，-3指定了倒数第三个元素，slice不会修改调用的数组

#### (6) splice() 

 返回被一个由删除元素组成的数组

​	在数组中插入和删除元素的通用方法，会修改其调用的数组

​	splice()能从数组中删除元素，插入元素到数组中或者同时完成两种操作。在插入或 删除点后的数组会根据需要增加或减少他们的索引值，因此数组的其它部分仍然保持连续。

​	第一个参数：指定了插入和删除的起始位置

​	第二个参数：指定了删除的元素的位置，如果省略则从起始位置到数组末尾都将被删除

​	后面任意参数指定了需要插入到数组中的元素	

#### (7) push()和pop()

​	将数组当栈使用

​	push()在数组 末尾添加一个或多个元素并返回新的数组长度，

​	pop()删除数组最后一个元素，减小数组长度，并返回它删除的值。

#### (8) `unshift()`和shift()

​	unshift()在数组的头部添加一个或多个元素，并将已存在的元素移到更高索引的位置来获得足够的空间，最后返回数组新的长度

​	shift()删除数组的第一个元素并返回，然后将所有随后的元素下移一个位置来填补数组头部的空缺

#### (9) `toString()`和`toLocaleString()`

​	toString()将数组每个元素转化成字符串，并输出用逗号分隔的字符串列表

​	toLocalString()是toString()的本地化方法，将每个数组元素转化为字符串，并使用本地化方法（和自定义实现的）分隔符将这些字符串连接起来生成最终的字符串



### `ECMA5`方法

#### (1) `forEach()`         

遍历数组，为每个元素调用指定的函数，函数三个参数为：数组元素、数组元素索引，数组本身，后面两个参数可省略

```
demo:
const arr =  ["aa",  "bb"];
const sum = 0；
arr.forEach((value, item, arr) => {
	sum += value;	
});
```

#### (2) map()		

调用数组的每个元素给指定的函数，并返回一个数组，包含每次调用该函数的返回值

`const arr = [3, 4, 7, 8];`

`const res = arr.map((value) => { return value*vavlue })`

#### (3) ilter()		

调用数组的每个元素给指定函数，返回数组的子集，子集元素符合函数逻辑判断

​		注意：filter()会跳过稀疏数组中缺少的元素，返回的数组总是稠密的

#### (4) every()和some()  

对数据进行逻辑判断，调用数组元素给指定函数，返回true或false

​		every()调用元素给指定函数，每个回调函数返回true后，every()才返回true

​		some()调用元素给指定函数，当存在回调函数返回true后，some()返回true，遍历所有元素后，回调函数返回的都是false,才返回false

​		every()、some()与filter不同，返回值不同

#### (5) reduce()和reduceRight()	

使用指定的函数，对数据元素进行组合，生成单个值	

#### (6) indexOf()和lastIndexOf()



### ECMA6方法

#### (1) 扩展运算符

#### (2) `Array.from`()

#### (3) `Array.of`()

#### (4) `copyWithin()`

#### (5) `find()和findIndex()`

#### (6) `fill()`

#### (7) entries()，keys()和values()`

#### (8) includes()

#### (9) `flat()、flatMap()`

#### (10) 数组的空位

#### (11) Array.prototype.sort()的排序稳定性



### 数组类型判断

1、Array.isArray()

```javascript
Array.isArray(fruits)
```



2、使用构造属性

```
function isArray(x) {
	return x.constructor.toString().indexOf("Array") > -1;
}
```

3、instanceof

```javascript
let fruits = ["Bananna", "Orange", "Apple", "Mango"];
fruits instanceof Array
```







## 时间



## 函数



## 对象



## 正则表达式

### (一) 正则直接量创建

#### (1) 创建

直接量(包含在一对/之间的字符)

```
let reg = /pattern/flags;
```

#### (2) 修饰符

| 修饰符 | 描述                                                 |
| ------ | ---------------------------------------------------- |
| i      | 执行对大小写不敏感的匹配                             |
| g      | 执行全局匹配(查找所有匹配而非在找到第一个匹配后停止) |
| m      | 执行多行匹配                                         |

#### (3) 表达式

| 表达式 | 描述                     |
| ------ | ------------------------ |
| [abc]  | 查找方括号之间的任何字符 |
| [0-9]  | 查找任何从0-9的数字      |
| (x\|y) | 查找任何\|分隔的选项     |

#### (4) 元字符

| 元字符 | 描述                           |
| ------ | ------------------------------ |
| \d     | 0-9之间任意一个数字            |
| \w     | 数字，字母, 下划线 0-9 a-z A-Z |
| \s     | 空格或者空白                   |
| \D     | 除了\d                         |
| \W     | 除了\w                         |
| \S     | 除了\s                         |
| .      | 除了\n之外的任意一个字符       |
| \      | 转义字符                       |
| \|     | 或                             |
| ()     | 分组                           |
| \n     | 匹配换行符                     |
| \b     | 匹配边界                       |
| ^      | 限定开始位置                   |
| $      | 限定结束位置                   |
| [a-z]  | 任意字母,a-z中任何一个         |
| [^a-z] | 非字母                         |
| [abc]  | abc三个字母中任何一个          |

#### (5) 量词

| 量词   | 描述                                    |
| ------ | --------------------------------------- |
| n+     | 匹配至少包含一个n的字符串               |
| n*     | 匹配包含0个或多个n的字符串              |
| n?     | 匹配包含0个或1个n的字符串               |
| n{x}   | 匹配包含x个n的序列的字符串              |
| n{x,y} | 匹配包含x至y个n的序列的字符串           |
| n{x,}  | 匹配包含至少x个n的序列的字符串          |
| n$     | 匹配任何结尾为n的字符串                 |
| ^n     | 匹配任何开头为n的字符串                 |
| ?=n    | 匹配任何其后紧接指定字符串n的字符串     |
| ?!n    | 匹配任何其后没有紧接指定字符串n的字符串 |



### (二) 正则对象

#### (1) 构造函数

```
let reg = new RegExp(pattern, flags);
```

#### (2) RexExp对象属性

| 属性       | 描述                    |
| ---------- | ----------------------- |
| global     | RegExp对象是否具有标志g |
| ignoreCase |                         |
| lastIndex  |                         |
| multiline  |                         |
| source     |                         |



#### (3) RexExp对象方法

| 方法    | 描述                              |
| ------- | --------------------------------- |
| compile | 编译正则表达式                    |
| exec    | 检索字符串中指定的值,返回找到的值 |
| test    | 检索字符串中指定的值，返回true    |



#### (4) 支持正则表达式的String对象的方法

| 方法        | 描述                             |
| ----------- | -------------------------------- |
| constructor | 返回创建对象的数组函数的引用     |
| length      | 设置或返回数组中元素的数目       |
| prototype   | 使您能有能力向对象添加属性和方法 |

#### (5) Array对象方法



## 类型判断



# 同步和异步



## 同步和异步

异步：一个任务不是连续完成的，先做一部分然后去干其它的事然后在做另一部分

同步：自上而下，连续执行，不能插入其他任务

好处：节省资源和时间，如IO输入和输出中可以让cpu干其他的事情不必等待，请求后台后执行其他任务等到请求结果返回后再继续执行，提高工作效率

## 异步编程方法

### callback

​		回调函数就是把任务的第二部分或剩下来的几部分单独写在一个函数里，等重新执行这个任务后，就直接调用这个函数

### Generator函数

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



#### 二、用法



# 模块导入导出



## (一) CommonJS

exports和module.exports的区别

一个js文件为一个模块，module.exports始终为对外暴露的接口，它所指向的内存内容对外暴露，可以修改，因为对外暴露的是它的地址，然后获取其引用

exports初始指向module.exports所指向的内容，如果对齐重新赋值，则改变了指针指向的内存区域，则变成了普通值，不再对外暴露。

```
// 导出 ex01.js
exports.name = "你好";
exports.height = 178;
exports = {
	age: 10
}
module.exports = {
	newName: '你好，新属性'
}

// 导出 ex02.js
exports.name = "你好";
exports.height = 178;
exports = {
	age: 10
}
module.exports.newName= '你好，新属性'
// test.js
const ex01 = require('ex01.js');
const ex02 = require('ex02.js');
console.log(ex01);  // res:   { newName: '你好，新属性' }
console.log(ex02);  // res: { name: '你好', height: 178, newName: '你好，新属性'}
```



## (二) `ES6 Module`

主要谈谈export default 这个坑，反正我用着不爽，最好先定义变量，然后用export 变量名导出，或直接使用export default value

如果要同时导出默认和其它值使用大括号，里面第一个为default, 取别名

`import { default as b, orgAddress } as './ex04'` 

```
// export用法 ex01.js
export const name = '张三';
export const age = 23;

// ex02.js
const name = '张三';
const age = 18;
export { name, age };

// ex03.js
export default "你好，世界";

// ex04.js
export default "家里蹲";
export let orgAddress = "杭州";
ggfgsdfhfh
// import用户 test01.js
import { name, age } from './ex01'
import * as re from './ex01.js'
console.log(name + ',' + age);     // 张三,23
console.log(re.name + ',' + re.age); // 张三，23

// test02.js
import { name, age } from './ex01'
import * as re from './ex01'
console.log(name + ',' + age);
console.log(re.name + ',' + re.age);

// test03.js
import { name } from './ex03';
import re from './ex03';
console.log(name); // error exports.default = name = "你好，世界";
console.log(re);  // 你好，世界

// test04.js
import a from './ex03';
import { default as b, orgAddress } as './ex04'  // 导入默认和其它值
console.log(a); // 家里蹲
console.log(orgAddress);  //

```

## (三) AMD



## (四) UMD



## (五) 不同模块打包



# 客户端`JS`

## windows

## document

### HTML文档对象模型

节点属性



`nodeType`

`nodeName`

节点种类:

- 元素节点

- 文本节点

- 属性节点

## HTTP

XMLHttpRequest

### 创建请求对象

```javascript
// 创建请求对象

// 处理响应
/**
* 
*/

// 发送请求


```



### 处理响应

`readyState`属性

- 0: 未初始化
- 1: 正在加载
- 2: 加载完毕
- 3: 正在交互
- 4: 完成

`responseText`

`responseXML`



### 发送请求



# 常见问题

## 变量提升

```javascript
console.log(a)		// undefined
var a = 0;
console.log(a)   // 0
function testa() {
	console.log(a); // undefined
	var a = 3;
	console.log(a) //3
}
testa();
/*
执行顺序：
​	1、声明变量a,;

​	2、声明函数testa; 

​	3、打印a,已声明未定义，undefined;

​	4、执行赋值a=0;

​	5、打印a,已赋值， 0

​	6、执行函数testa(),进入函数testa()，同样先声明后执行，优先在当前作用域内查找

​	7、开辟内存空间,先声明变量a

​	8、打印a,优先在当前作用域内查找，找到变量a, undefined

​	9、赋值

​	10、打印变量a

*/
```

