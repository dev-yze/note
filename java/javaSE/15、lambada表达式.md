### 一、lambda简介

#### 1、了解lambda表达式概念

​		lambda即λ，匿名函数的意思。lambda表达式本质上是定义一个匿名内部类。即定义一个匿名函数的同时定义一个匿名内部类

​		lambda表达式，也可成为闭包，是java8最重要的新特性之一，lambda允许把函数作为一个方法的参数使用，使用lambda表达式可以使代码更加简洁紧凑，其实lambda表达式本质只是一个语法糖，由编译器推断转换为常规的代码。因此可以使用更少的代码来实现相同的功能。

#### 2、lambda语法

```java
(parameters) -> expression
(parameters) -> { statements; }
```



#### 3、表达式特征

- 可选声明类型
- 可选的参数圆括号
- 可选的大括号
- 可选的返回关键字

demo:

```
// 不需要参数，返回值是5
() -> 5
// 接收一个参数，返回其2倍的值
x -> 2*x
// 接收两个参数，并返回两者差
(x, y) -> x - y
// 接收两个int型参数，返回两者的和
(int x, int y) -> x + y
// 接收一个string对象,并在控制台打印，不反会任何值
（String s） -> System.out.println(s)

```

#### 4、lambda表达式使用

lambda表达式本质就是匿名内部类的使用

现有一个接口，其有一个抽象方法,分别通过匿名内部类和lambda表达式来实现该接口

```
/** 接口，具有一个抽象方法
 * @description
 * @author zhangen.yang
 * @date: 2019年12月29日下午4:56:56
 */
public interface Ability {
	void doAbility(String token);
}

package course10_lambda;

import course10_lambda.interfa.Ability;

/**
 * @description 测试
 * @author zhangen.yang
 * @date: 2019年12月29日下午4:57:56
 */
public class TestCode {
	public static void main(String[] args) {
		// 使用匿名内部类，可以不通过定义子类或实现类，直接获得子类对象或实现类对象
		Ability ability = new Ability() {

			@Override
			public void doAbility(String token) {
				// TODO Auto-generated method stub
				System.out.println(token);
				System.out.println("我是一只小小鸟啊，我要飞得更高！！！！");
			}
		};
		ability.doAbility("开始使用匿名内部类实现");
		
		// 通过lambda表达式实现接口子类
		Ability ab = (token) -> {
			System.out.println(token);
			System.out.println("我是一只自由的鸟");
		};
		ab.doAbility("开始使用lambda表达式实现");
	}

}

```



5、lambda表达式作用域

​	在lambda表达式中访问外层的局部变量，但在lambda表达式内部不能修改定义在lambda表达式外部的局部变量，否则会编译报错

​	lambda表达式的局部变量可以不用声明为final，但是必须不可被后面的代码修改（即隐性的具有final定义）。在lambda表达式中不允许声明一个与外部变量同名的参数或者局部变量



二、lambda表达式的使用

1、在线程中使用



2、在集合中使用



3、在流中使用