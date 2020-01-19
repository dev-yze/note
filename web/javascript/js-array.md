### 一、数组基本属性（概念、操作、注意）

#### 1、数组的创建

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

  

#### 2、增删改查

​	读和写：

​		使用[]操作符来访问数组中的一个元素，数组的引用位于方括号的左边，方括号中是一个返回非负整数的任意表达式，使用该语法既可以读又可以写一个数组元素

```javascript
var a = ['world'];   // 从一个元素的数组开始
var value = a[0];    // 读取第0个元素
a[1] = 3.14;		// 写入第1个元素
let i = 2;
a[i] = 3;            // 写入第2个元素
```

​	注意：数组是对象的特殊形式，使用方括号访问数组元素就像用方括号访问对象的属性一样。JavaScript将指定的数字的索引值转换成字符串，索引值1编程“1”，然后将其作为属性名来使用。

​			数组特别之处在于，当使用小于2³²的非负整数作为属性名时数组会自动维护其length属性值。

​			数组的索引和对象的属性名：所有的索引都是属性名，但只有在0~2³²-2之间的整数属性名才是索引，所有的数组都是对象，可以为其创建任意名字的属性。但如果使用的属性是数组的索引，数组的特殊行为将根据需要更新它们的length属性值

​		注意：可以使用负数和非整数来索引数组，这种情况下，数值转换为字符串，字符串作为属性名来用，当作常规的对象属性，而非数组的索引。同样如果凑巧使用了非负整数的字符串，它就当做数组的索引，而非对象属性。当使用一个浮点数和一个整数相等时也一样

​		故：js中数组仅是对象属性名的一种特殊类型，在js数组中没有越界的错误概念，当试图查询任何对象中不存在的属性时，不会报错，只会得到undefined值，类似于对象，对象中同样存在这种情况

​	

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



### 3、数组长度

​	

```javascript
let a = [];
a.length()  // 数组的长度
```

#### 4、稀疏数组和多维数组

​	稀疏数组：稀疏数组就是包含从0开始的不连续索引的数组。稀疏数组length属性值大于元素的个数

#### 5、数组遍历

- ​	使用for循环,可以根据需要从头部或者末尾进行遍历

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

### 二、ECMA3数组方法

#### 1、join()	将数组元素转化为字符串连接在一起，返回最后生成的字符串,可指定连接符参数，默认逗号

#### 2、reverse()  将数组中的元素颠倒排序，返回逆序数组

#### 3、sort()	将数组中的元素排序并返回排序后的数组

#### 4、concat()

​	创建并返回一个新数组，它的元素包括调用concat()的原始数组的元素和concat()的每个参数，如果这些参数中任何一个自身是数组，则连接的是数组的元素。但concat()不会递归扁平化数组，concat()也不会修改调用的数组。

#### 5、slice()  返回指定提取的数组片段

​	返回指定数组的一个片段或数组，它的参数分别指定了片段的开始和结束的位置，返回的数组包含第一个参数指定的位置和所有到但不含第二个参数指定的位置之间的数组元素，如果只指定一个元素，返回数组包含从开始位置到数组结尾的所有元素，如参数中出现负数，它表示相对于数组中最后一个元素的位置，如-1指定了最后一个元素，-3指定了倒数第三个元素，slice不会修改调用的数组

#### 6、splice()  返回被一个由删除元素组成的数组

​	在数组中插入和删除元素的通用方法，会修改其调用的数组

​	splice()能从数组中删除元素，插入元素到数组中或者同时完成两种操作。在插入或 删除点后的数组会根据需要增加或减少他们的索引值，因此数组的其它部分仍然保持连续。

​	第一个参数：指定了插入和删除的起始位置

​	第二个参数：指定了删除的元素的位置，如果省略则从起始位置到数组末尾都将被删除

​	后面任意参数指定了需要插入到数组中的元素	

#### 7、push()和pop()

​	将数组当栈使用

​	push()在数组 末尾添加一个或多个元素并返回新的数组长度，

​	pop()删除数组最后一个元素，减小数组长度，并返回它删除的值。

#### 8、unshift()和shift()

​	unshift()在数组的头部添加一个或多个元素，并将已存在的元素移到更高索引的位置来获得足够的空间，最后返回数组新的长度

​	shift()删除数组的第一个元素并返回，然后将所有随后的元素下移一个位置来填补数组头部的空缺

#### 9、toString()和toLocaleString()

​	toString()将数组每个元素转化成字符串，并输出用逗号分隔的字符串列表

​	toLocalString()是toString()的本地化方法，将每个数组元素转化为字符串，并使用本地化方法（和自定义实现的）分隔符将这些字符串连接起来生成最终的字符串





### 三、ECMA5方法(遍历、映射、过滤、检测、 简化、搜索)

#### 1、forEach()         遍历数组，为每个元素调用指定的函数，函数三个参数为：数组元素、数组元素索引，数组本身，后面两个参数可省略

```
demo:
const arr =  ["aa",  "bb"];
const sum = 0；
arr.forEach((value, item, arr) => {
	sum += value;	
});
```

#### 2、map()		调用数组的每个元素给指定的函数，并返回一个数组，包含每次调用该函数的返回值

`const arr = [3, 4, 7, 8];`

`const res = arr.map((value) => { return value*vavlue })`

#### 3、filter()		调用数组的每个元素给指定函数，返回数组的子集，子集元素符合函数逻辑判断

​		注意：filter()会跳过稀疏数组中缺少的元素，返回的数组总是稠密的

#### 4、every()和some()  对数据进行逻辑判断，调用数组元素给指定函数，返回true或false

​		every()调用元素给指定函数，每个回调函数返回true后，every()才返回true

​		some()调用元素给指定函数，当存在回调函数返回true后，some()返回true，遍历所有元素后，回调函数返回的都是false,才返回false

​		every()、some()与filter不同，返回值不同

#### 5、reduce()和reduceRight()	使用指定的函数，对数据元素进行组合，生成单个值	

#### 6、indexOf()和lastIndexOf()





### 四、ECMA6方法

1、扩展运算符

2、Array.from()

3、Array.of()

4、数组实例的copyWithin()

5、数组实例的find()和findIndex()

6、数组实例的fill()

7、数组实例的entries()，keys()和values()

8、数组实例的includes()

9、数组实例的flat()、flatMap()

10、数组的空位

11、Array.prototype.sort()的排序稳定性



### 五、判断数组

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





