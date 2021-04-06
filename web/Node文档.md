# 模块化开发

1、



2、



3、global对象

node.js中，global对象定义了全局命名空间，定义了一个全局变量时，这个变量会成为global的属性即在全局作用域中，任何变量、函数和对象都是global对象的一个属性值





4、模块作用域（require, exports, module.exports）

node中使用模块化编程思想，以便造成变量和函数的污染

`require('path')`：用于获取一个模块的接口, 即模块的exports对象

`exports或module.exports`：向外开放变量、函数

exports：初始值为{}，不可单独定义，只能返回一个object对象

```
// base.js
exports = ['a', 'b', 'c'];
// test.js
let baseModule = require('./base');
console.log(baseModule);
console.log(baseModule.length);
结果：
{}
undefined
```

module.exports: 初始值为{}，可单独定义，返回数据类型

```
// base.js
exports = ['a', 'b', 'c'];
// test.js
let baseModule = require('./base');
console.log(baseModule);
console.log(baseModule.length);
结果：
[ 'a', 'b', 'c' ]
3
```

5、全局可用变量、函数和对象

`1.`全局作用域

node.js中，global对象定义了全局命名空间，定义了一个全局变量时，这个变量会成为global的属性即在全局作用域中，任何变量、函数和对象都是global对象的一个属性值

`2.`全局可用

node.js中提供的一些全局可用的变量、函数和对象，这里所谓全局就是不需要进行模块加载，可以直接使用，其中包括全局作用域的函数和对象，也包括另一种不在全局作用域，而是在每个模块作用域中都存在的变量、函数和对象，在全局可用，但不在global对象的属性

3、`_dirname`和`_filename`变量

4、全局函数

5、console对象

# 输入和输出



一、文件读写操作

1、引入fs模块

```javascript
let fs = require('fs');
```

2、文件写入

```
// 同步文件写入
{
    try {
        console.log('写入文件....');
        fs.writeFileSync('G:\\workspce\\vscode\\yang-node\\file\\a.txt', '黑马程序员dddddddd');
    } catch(e) {
        console.log('不好意思，写入文件失败');
    }
    console.log('我是最后一行');
}

// 异步文件写入
{
    console.log('异步写入文件...');
    fs.writeFile('G:\\workspce\\vscode\\yang-node\\file\\a.txt', '开始写入了', function(err) {
        if(err) {
            console.log('不好意思，写入文件失败');
            return;
        }
        console.log('写入成功')
    })
    console.log('我是最后一行');
}
// 向文件追加内容
{
    let data = '我是追加的内容222';
    console.log('向文件追加内容');
    fs.appendFile('G:\\workspce\\vscode\\yang-node\\file\\a.txt', data, function(err) {
        if (err) {
            console.log('追加文件失败了');
            return;
        }
        console.log('追加文件成功');
    })
    console.log('我是最后一行');
}
```

3、文件读取

```
/**
 * 读取文件
 */
{
    console.log('开始异步读取文件')
    fs.readFile('G:\\workspce\\vscode\\yang-node\\file\\a.txt', function (err, data) {
        if (err) {
            return console.log('文件读取失败');
        }
        console.log('读取成功，内容是:\n'+data.toString());
    })
    console.log('我是最后一行');
}
```



二、文件相关信息操作

1、获取文件信息

```javascript
/**
 * 获取文件信息
 */
{
    fs.stat('G:\\workspce\\vscode\\yang-node\\file\\a.txt', function (err, stats) {
        if (err) {
            return console.log('获取文件信息失败\n' + err)
        }
        console.log('获取文件信息成功，开始判断文件信息')
        // 判断是否是文件
        console.log('是否是文件：' + stats.isFile());
        // 输出文件信息
        console.log(stats);
    })
}
```

三、利用Buffer缓冲区处理数据

Buffer缓冲区用来存储二进制数据，通过不同字符编码将二进制数据转为字符。

注意：Buffer缓冲区大小限制在1GB，超过1GB的文件无法直接完成读写操作

1、创建Buffer缓冲区

```
// 通过buffer构造函数来存储二进制数据
let buf = new Buffer(array)				// 数组
		  new Buffer(buffer)			// buffer对象
		  new Buffer(arrayBuffer[, byteOffset[,length]])
		  new Buffer(size)   			// 字节
		  new Buffer(str[, encoding])   // 字符串
```

2、读取

```
buf.toString([encoding[, start[, end]]])
```

3、写入

```
buf.write(String[, offset[, length]][, encoding])
```

4、操作

拼接缓冲区

```
buf.concat(lsit[,totalLength])
```

四、利用Stream处理数据

1、流概念和类型

2、可读流和可写流

3、使用pipe()处理大文件





# 网络编程



# 异步编程



# `npm`命令

1、添加ES6支持

```javascript
// 1、初始化npm工作目录，生成package.json文件
npm init -y
// 2、安装babel-cli
npm install babel-cli --save 或 npm install babel-cli --g
// 3、安装babel-preset-es2015支持ES6的语法
npm install babel-preset-es2015 --save
// 添加名为.babelrc的配置文件
{
    "presets": [
        "es2015"
    ],
    "plugins": []
}
```

2、