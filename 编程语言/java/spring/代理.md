### 一、代理模式

​		代理模式：代理模式是23种设计模式的一种，他是指一个对象A通过持有另一个对象B，可以具有B同样的行为模式，为了对外开放模式，B往往实现了一个接口，而A也会去实现这个接口，但B是真正实现类，A比较虚，他借用了B的方法去实现接口的方法。A虽然是“伪军"，但它可以增强B，在调用B的前后做些其它的事情。SpringAOP就是使用了动态代理完成了代码的动态”织入“。

使用代理的好处：

​		如果一个工程依赖另一个工程的接口，但是另一个工程的接口不稳定，经常变更协议，就使用一个代理，接口变更时，只需要修改代理，不需要修改业务代码，从这个意义上说，所有调用外界的接口，我们都可以这么做，不让外界的代码对我们有入侵，这叫防御式编程，代理其他的应用可能还有很多。

代理的类型：如果上面类A写死持有B，就是B的静态代理，如果A代理的对象是不确定的，就是动态代理.

​	静态代理：由程序员或特定工具自动生成源代码再对其编译，在程序运行前代理类的.class文件就存在了，

​	动态代理：在程序运行时用反射机制动态创建而成

#### 1、静态代理

​		在代理对象中引用目标对象且实现目标对象所实现的接口，在实现的接口方法中调用目标对象相同的实现方法，调用前后可进行日志拦截、数据统计、权限验证等操作。

#### 2、JDK动态代理

通过java.lang.reflect.Proxy类的静态方法newProxyInstance生成代理对象

```java
/**
* loader:目标类的类加载器
* interfaces: 目标类实现的全部接口
* invocationHandler h:得到InvocationHandler接口的子类的实例
*/
public static Object newProxyInstance(ClassLoader loader,
                                          Class<?>[] interfaces,
                                          InvocationHandler h)
        throws IllegalArgumentException{};
```

代理工厂实现java.lang.reflect.InvocationHandler接口

```java
package java.lang.reflect;

public interface InvocationHandler {

    /**
     * proxy : 被代理的对象
     * method ： 要调用的方法
     * args : 方法调用时所需的参数
     */

    public Object invoke(Object proxy, Method method, Object[] args)
        throws Throwable;
}

```

```java
package course09_proxy.type.jdkproxy;

import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

public class LogHandler implements InvocationHandler {
	
	private Object targetObject;
	
	public Object newProxyInstance(Object targetObject) {
		this.targetObject = targetObject;
		return Proxy.newProxyInstance(targetObject.getClass().getClassLoader(), targetObject.getClass().getInterfaces(), this);
	}

	@Override
	public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
		// TODO Auto-generated method stub
		System.out.println("日志开始--------->");
		for (int i = 0; i < args.length; i++) {
			System.out.println(args[i]);
		}
		Object ret = null;
		try {
			System.out.println("打印日志----------------------------------");
//			System.out.println(proxy);
			ret = method.invoke(targetObject, args);
			System.out.println("操作成功-----------------------------------");
		} catch (Exception e) {
			// TODO: handle exception
			e.printStackTrace();
			System.out.println("error----异常" + "\n" + e);
			throw e;
		}
		return ret;
	}
}

package course09_proxy.type.jdkproxy;
import course09_proxy.type.service.UserManagerService;
import course09_proxy.type.service.impl.UserManagerServiceImpl;
public class ProxyTest {
	public static void main(String[] args) {
		LogHandler logHandler = new LogHandler();
		UserManagerService userManagerService = (UserManagerService)logHandler.newProxyInstance(new UserManagerServiceImpl());
		userManagerService.addUser(111, "张三");
	}
	
}

```



#### 3、CGLIB动态代理

- 创建目标类（业务类）

- 创建拦截器，实现`net.sf.cglib.proxy.MethodInterceptor`接口

- 通过Enhancer类实例对象将目标类和拦截类，织入，创建代理类

  ```
  import java.lang.reflect.Method;
  import net.sf.cglib.proxy.MethodInterceptor;
  import net.sf.cglib.proxy.MethodProxy;
  /**
   * @description
   * @author zhangen.yang
   * @date: 2019年12月29日下午12:15:21
   */
  public class UserManagerServiceImplInterceptor implements MethodInterceptor {
  	/**
  	 * 拦截器
  	 * @description
  	 * @param o			要增强的对象
  	 * @param method	拦截的方法
  	 * @param objects	参数列表
  	 * @param methodProxy	方法的代理
  	 * @return
  	 * @throws Throwable
  	 */
  	@Override
  	public Object intercept(Object o, Method method, Object[] objects, MethodProxy methodProxy) throws Throwable {
  		// TODO Auto-generated method stub
  		System.out.println("--------------方法调用前处理--------------");
  		Object object = methodProxy.invokeSuper(o, objects);
  		System.out.println("---------调用后处理---------");
  		return object;
  	}
  }
  
  import net.sf.cglib.proxy.Enhancer;
  /** 测试生成代理
   * @description
   * @author zhangen.yang
   * @date: 2019年12月29日下午12:23:02
   */
  public class ProxyTest {
  	public static void main(String[] args) {
  		Enhancer enhancer = new Enhancer();
  		enhancer.setSuperclass(UserManagerServiceImpl.class);
  		enhancer.setCallback(new UserManagerServiceImplInterceptor());
  		UserManagerServiceImpl userManagerServiceImpl = (UserManagerServiceImpl) enhancer.create();
  		userManagerServiceImpl.addUser(222, "张三");
  	}
  }
  
  
  
  ```

### 二、AOP联盟

#### 1、AOP简介

​	AOP面向切面编程是一种编程技术，可以增强现有的中间环境或开发环境,是面向对象编程OOP的一种补充和完善。

​	AOP联盟定义了一套用于规范AOP实现的底层API，通过这些统一的底层的API，可以使各个AOP实现工具之间实现相互兼容，现在AOP联盟已有几个项目提供了AOP相关的技术，如通用代理，拦截器或字节码转换器

- ASM 轻量级字节码转换器
- AspectJ: 一个面向切面的框架，扩展了Java语言
- AspectWerkz： 一个面向切面的框架，基于字节码级别的动态织入和撇脂
- BCEL: 字节码转换器
- CGLIB：用于类工件操作和方法拦截的高级API
- Javassist:  具有高级API的字节码转换器
- JBoss-AOP:  拦截和基于元数据的AO框架



AOP将软件系统分为两部分:核心罗杰和横切逻辑。核心逻辑主要处理系统正常的业务逻辑，

横切逻辑不关注系统核心逻辑，其只关注与系统核心逻辑并非强相关的逻辑，如日志、权限控制等。

#### 2、AOP相关概念

- ​	横切关注点
- 切面(Aspect)
- 连接点(JoinPoint)
- 切入点(PointCut)
- 通知(Advice)
- 目标对象(Target Object)
- 织入(Weaving)
- 引入(Introduction)

#### 3、SpringAOP的实现

（1）通过jdk动态代理实现



（2）通过cglib实现



#### 4、增强类型



#### 5、切入点类型



### 三、Spring集成AspectJ



### 四、SpringAOP实现原理

