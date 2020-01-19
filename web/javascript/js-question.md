# 一、了解JS(背景、发展、变化、作用)

## 二、问题

## 1、变量提升和执行顺序

`console.log(a)		// undefined`
`var a = 0;`
`console.log(a)   // 0`
`function testa() {`
	`console.log(a); // undefined`
	`var a = 3;`
	`console.log(a) //3`
`}`
`testa();`

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