#### 一、AOP概述

AOP: Aspect Oriented Programming, 面向切面编程，将非核心业务如日志等从不同的纵向操作中抽取出来。

AOP是通过代理的方式在业务处理方法前后增强

代理一般有静态代理和动态代理：静态代理、JDK动态代理、CGLIB动态代理

##### 1、JDK动态代理

​		JDK动态代理基于接口

##### 2、CGLIB动态代理

#### 二、AOP实现

##### 1、使用ProxyFactoryBean

- 编写和实现业务接口
- 编写通知类实现MethodInterceptor接口，实现invoke方法
- 配置ProxyFactoryBean

```java
// 业务类省略.....
import java.text.SimpleDateFormat;
import java.util.Date;
import org.aopalliance.intercept.MethodInterceptor;
import org.aopalliance.intercept.MethodInvocation;
import org.springframework.stereotype.Component;
// 通知
@Component
public class AopLogServiceImpl implements MethodInterceptor {
	private SimpleDateFormat sd = new SimpleDateFormat("yyyy-mm-dd HH:mm:dd");	
	@Override
	public Object invoke(MethodInvocation tar) throws Throwable {
		// TODO Auto-generated method stub
		System.out.println("【" + sd.format(new Date()) + "】方法执行开始");
		Object obj = tar.proceed();
		System.out.println("【" + sd.format(new Date()) + "】方法执行结束");
		return obj;
	}
	
}
```

```
// xml配置

<!-- 扫描组件 -->		
	<context:component-scan base-package="com.spring.dev"></context:component-scan>
	<!--
		配置proxyFactoryBean属性
			1、配置代理接口  proxyInterfaces
			2、代理接口实现类  target
			3、通知   interceptorNames
	-->
	<bean id="proxyFactoryBean" class="org.springframework.aop.framework.ProxyFactoryBean">
		<property name="proxyInterfaces">
			<value>com.spring.dev.service.user.UserService</value>
		</property>
		<property name="target">
			<ref bean="userServiceImpl" />
		</property>
		<property name="interceptorNames">
			<list>
				<value>aopLogServiceImpl</value>
			</list>
		</property>
	</bean>
```

2、

#### 三、AspectJ

##### 1、简介

​		AspectJ: java社区里最完整最流行的AOP框架

​		在Spring2.0版本以上，可以使用基于AspectJ注解或基于XML配置的AOP

##### 2、Spring中启用AspectJ注解支持

- 导入jar包

- 引入命名空间

- 配置

  ```
  <aop:aspectj-autoproxy></aop:aspectj-autoproxy>
  ```

  当SpringIOC容器侦测到bean配置文件中的<aop:aspectj-autoproxy>元素时，会自动为与AspectJ切面相匹配的bean创建代理

##### 3、用AspectJ注解声明切面

- SpringIOC容器中声明AspectJ切面，首先将切面声明为Bean实例，然后使用@Aspect注解将该类声明为切面
- AspectJ中包含许多通知，通知是带有某种注解的方法，根据注解在不同时间段执行，来增强业务方法
- AspectJ支持5种类型的注解
  - @Before : 前置增强通知, 在方法执行之前执行
  - @After : 后置通知，在方法执行之后执行
  - @AfterReturning : 后置增强通知
  - @AfterThrowing ：异常通知，在方法抛出异常后执行
  - @Around ： 环绕通知，围绕着方法执行

4、AspectJ使用

```
package com.spring.dev.common.log;
import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.AfterThrowing;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Pointcut;
import org.springframework.stereotype.Component;
@Component
@Aspect
public class LogServiceImpl {	
	/**
	 * 切入点
	 */
	@Pointcut("execution(* com.spring.dev.service.*.*.*(..))")
	public void pointCut() {
	}
	/**
	 * 前置通知
	 */
	@Before("pointCut()")
	public void before(JoinPoint joinPoint) {
		System.out.println("【Log before】 方法执行之前" + joinPoint.getSignature().getName());
	}
	/**
	 * 后置通知
	 */
	@After("pointCut()")
	public void after() {
		System.out.println("【Log after】 方法执行之后");
	}
	/**
	 * 后置增强
	 */
	@AfterReturning("pointCut()")
	public void afterReturning() {
		System.out.println("【Log afterReturning】 方法执行之后");
	}
	/**
	 * 环绕通知
	 */
	@Around("pointCut()")
	public int around(ProceedingJoinPoint joinPoint) {
		try {
			System.out.println("【log around】 开始");
			joinPoint.proceed();
			System.out.println("【log around】 结束");
		} catch (Throwable e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return 0;
	}
	/**
	 * 抛出异常
	 */
	@AfterThrowing("pointCut()")
	public void afterThrowing() {
		System.out.println("【Log afterThrowing】 方法执行之后");
	}
}
```

执行结果:

![image-20200401135913175](C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200401135913175.png)



#### 四、AOP概念详解

##### 1、切入点表达式

​	作用：通过表达式的方式**定位**一个或多个具体的**连接点**

###### 	1）切入点表达式语法

```
execution([权限修饰符][返回值类型][简单类名/全类名][方法名](参数列表))
```

​	2）案例

| 表达式 | execution(***** com.atguigu.spring.ArithmeticCalculator.*****(**..**)) |
| ------ | ------------------------------------------------------------ |
| 含义   | 匹配`ArithmeticCalculator`接口种声明的所有方法                                                                                   第一个\*代表任意修饰符及任意返回值                                                                                                                   第二个\*表任意方法                                                                                                                                                      ..匹配任意数量、类型参数                                                                                                                                       若目标类、接口与该切面在同一个包种可以省略包名 |



##### 2、连接点细节（JoinPoint）

###### 1）概念

​		切入点表达式通常都是宏观上定位一组方法，和具体某个通知的注解结合起来就能够确定对应的连接点。就一个具体的连接点而言，我们关心这个连接点的一些具体信息，如，当前连接点所在方法的方法名、当前传入的参数值等。这些信息都封装在`JointPoint`接口的实例对象中

###### 2）JoinPoint

<img src="C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200401142120807.png" alt="image-20200401142120807" style="zoom: 67%;" />



![image-20200401131246820](C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200401131246820.png)

###### 3）ProceedingJoinPoint



##### 3、通知

###### 1）概述

- 在具体的连接点上要执行的操作
- 一个切面可以包含多个通知
- 通知所使用的注解的值往往是切入点表达式

###### 2）前置通知

###### 3）后置通知

###### 4）返回通知

###### 5）异常通知

###### 6）环绕通知

- 环绕通知是所有通知中功能最为强大的，能全面地控制连接点，甚至可以控制是否执行连接点
- 对于环绕通知来说，连接点的参数类型必须是ProceedingJoinPoint,它是JoinPoint的子接口，允许控制何时执行，是否执行连接点
- 在环绕通知中需要明确调用ProceedingJoinPoint的proceed()方法来执行被代理的方法。如果忘记会导致通知执行了，而代理方法未执行
- 注意：环绕通知需要返回目标方法执行后的结果，即调用proceedingJoinPoint.proceed()的返回值，否则出现空指针异常

##### 4、切入点表达式重复使用

1. 在编写AspectJ切面时，可以直接在通知注解中写入切入点表达式，但同一个切点表达式可能会在多个通知中重复出现
2. 在AspectJ切面中，可以通过@Pointcut注解将一个切入点声明成简单的方法，切入点的方法体通常是空的，因为将切入点定义未应用程序逻辑混在一起不合理
3. 切入点方法的访问控制符同时也控制着这个切入点的可见性。如果切入点要在多个切面中共用，最好将它们集中在一个公共的类中，在这种情况下，它们必须声明为public。在引入这个切入点时，必须将类名也包括在内。如果没有与这个切面放在同一个包中，还必须包含包名
4. 其他通知可以通过方法名称引入该切入点

```java
// 定义公共切入点类
package com.spring.dev.common.log;
import org.aspectj.lang.annotation.Pointcut;
public class LogPointCut {
	/**
	 * 新增类方法切入点
	 */
	@Pointcut("execution(* *.add*(..))")
	public void add() {}
}

// 引用切入点类切入点
	/**
	 * 前置通知
	 */
	@Before("com.spring.dev.common.log.LogPointCut.add()")
	public void before(JoinPoint joinPoint) {
		System.out.println("【Log before】 方法执行之前" + joinPoint.getSignature().getName());
	}
```



##### 5、指定切面的优先级

- 在同一个连接点上应用不止一个切面时，除非明确指定，否则它们的优先级不确定
- 切面的优先级可以通过实现Ordered接口或利用@Order注解指定
- 实现Ordered接口，getOrder()方法的返回值越小优先级越高
- 若使用@Order注解，序号出现在注解中

五、用XML配置切面





增强类型

AOP联盟定义了org.aopalliance.aop.Advice接口，Spring支持5种类型的增强，Spring AOP支持很懂增强类型，Spring AOP按增强类型在目标方法中的连接点位置可以分为5种

- 前置增强
- 后置增强
- 环绕增强
- 异常抛出增强
- 引介增强

前置增强



​	![image-20200401131246820](C:\Users\18856\AppData\Roaming\Typora\typora-user-images\image-20200401131246820.png)