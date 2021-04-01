# 一、JS基础

变量

字符串

分支

循环

数组

函数

对象

数据结构

异步

class

文件



# 二、客户端JS

## windows

## document

### HTML文档对象模型

节点属性



nodeType

nodeName

节点种类:

- 元素节点

- 文本节点

- 属性节点



### 获取文档对象

- `document.getElementById("#id")`
- `document.getElementByClass`
- `document.getElementByTagName('tagName')`



parentNode

### 查询和设置属性

```javascript
var eleNode = document.getElementById('#idname');
eleNode.setAttribute("propName", value);
eleNode.getAttribute("propName");

```

### 创建添加节点

```javascript
// document.createElement(nodeName) 	创建元素节点
// document.createTextNode(text) 		创建文本节点

// parent.appendChild(child)
// brother.insertBefore(newElement, targetElement)		在已有元素节点前添加新元素


var cEle = document.createElement("p");
var textNode = document.createTestNode("Hello Node");
var body_ele_node = document.getElementByTagName("body");
body_ele_node.appendChild(cEle);
cEle.appendChild(textNode);
```



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

readyState属性

- 0: 未初始化
- 1: 正在加载
- 2: 加载完毕
- 3: 正在交互
- 4: 完成

responseText

responseXML



### 发送请求







# 三、案例