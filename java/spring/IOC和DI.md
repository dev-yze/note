#### 一、IOC (控制反转)

##### 1、概念

​		反转了资源获取方向，将bean的生命周期由容器管理，容器会主动将资源推给需要的组件，开发人员不需要知道容器如何创建对象，可以直接拿来用

##### 2、DI：依赖注入

​		IOC的另一种表达方式，即组件以一些预先定义好的方式(如setter)接受容器的资源注入（Spring中组件就是其管理的对象）

​		IOC就是反转控制的思想，DI是对IOC的一种具体实现

##### 3、IOC容器在Spring中的实现

​		前提：Spring中有IOC思想，IOC思想必须基于IOC容器来完成，而IOC容器最底层的本质就是一个对象工厂

- 在IOC容器读取Bean的实例之前，需要将IOC容器本身实例化
- Spring提供了IOC容器的两种实现方式
  - BeanFactory: IOC容器的基本实现，是Spring内部的基础设施，是面向Spring本身的，不是提供给开发人员使用的
  - ApplicationContext: BeanFactory的子接口，提供了更多高级特性，面向Spring的使用者

##### 4、ApplicationContext的主要实现类

- ClassPathXmlApplicationContext
- FileSystemXmlApplicationContext
- 在初始化时创建单例的Bean，也可以通过配置的方式指定创建的Bean是多例的

5、`ConfigurableApplicationContext`

- 是`ApplicationContext`的子接口，包含一些扩展方法
- refresh()和close()让ApplicationContext具有启动、关闭和刷新上下文的能力

![](F:\Users\ZhangEn\Pictures\learn\java\spring\ApplicationContextImpl.jpg)

6、WebApplicationContext

​	专门为web应用而准备的，它允许从相对于WEB根目录的路径中完成初始化工作

7、容器的结构图



#### 二、Bean操作

##### 1、获取bean

- 通过id
- 通过类型
- 通过id和类型

```java
// 获取Bean通过id
	public static void getBeanById() {
		// 通过ClassPathXmlApplicationContext加载配置文件
		ApplicationContext ac = new ClassPathXmlApplicationContext("applicationContext.xml");
		Person person = (Person) ac.getBean("person");
		person.setAge(13);
		person.setName("张三");
		System.out.println(person);
	}
	
	// 通过bean类型获取，如果同一个类型在xml文件中配置了多个，则获取会抛出异常,所以根据类型获取bean必须是单例，在容器中唯一
	public static void getBeanByType() {
		// 通过FileSystemXmlApplicationContext加载配置文件
		ApplicationContext ac = new FileSystemXmlApplicationContext("G:\\workspce\\eclipse-workspace\\spring-project\\resource\\applicationContext.xml");
		Person person = (Person) ac.getBean(Person.class);
		person.setAge(13);
		person.setName("李四");
		System.out.println(person);
	}
	
	// 同时通过id和bean类型
	public static void getBeanByIdAndType() {
		ApplicationContext ac = new FileSystemXmlApplicationContext("G:\\workspce\\eclipse-workspace\\spring-project\\resource\\applicationContext.xml");
		Person person = (Person) ac.getBean("person", Person.class);
		person.setName("王五");
		person.setAge(23);
		System.out.println(person);
	}
```



##### 2、bean属性赋值

- 通过bean的setXxx()方法赋值

  ```xml
  <bean id="person" class="com.spring.dev.dao.entity.Person">
      <property name="name" value="嘿嘿"></property>
      <property name="age" value="20"></property>
  </bean>
  ```

  

- 通过bean的构造器赋值

  ```xml
  	<!-- 通过构造方法配置 -->
  	<bean id="person" class="com.spring.dev.dao.entity.Person">
  		<!-- <constructor-arg value="构造"></constructor-arg>
  		<constructor-arg value="20"></constructor-arg> -->
  		<!-- 通过index确定参数顺序 -->
  		<!-- <constructor-arg value="45" index="1"></constructor-arg>
  		<constructor-arg value="index索引名" index="0"></constructor-arg> -->
  		<!-- 通过通过类型确定参数顺序 -->
  		<constructor-arg value="45" index="1" type="java.lang.Integer"></constructor-arg>
  		<constructor-arg value="index索引名" index="0" type="java.lang.String"></constructor-arg>
  	</bean>
  ```

  

- p名称空间

  ```XML
  <!-- p命名空间 -->
  	<bean id="person" class="com.spring.dev.dao.entity.Person" p:name="命名空间" p:age="34"></bean>
  ```

- 可以使用的值

  - 字面量

    - 可以使用字符串表示的值，可以通过value属性或value子节点的方式指定
    - 基本数据类型及封装类、String等类型都可以采取字面值注入的方式
    - 若字面值中含有特殊字符，可以使用`<![CDATA[]]>`把字面值包裹

  - null值

    ```xml
    <bean id="person" class="com.spring.dev.dao.entity.Person">
        <property name="name">
            <null></null>
        </property>
        <property name="age" value="20"></property>
    </bean>
    ```

    

  - 给bean的级联属性赋值

    ```xml
    <!-- bean的级联属性赋值 -->
    	<bean id="student" class="com.spring.dev.dao.entity.Student"></bean>
    	<bean id="person" class="com.spring.dev.dao.entity.Person">
    		<property name="name" value="张三"></property>
    		<property name="age" value="16"></property>
    		<property name="student" ref="student"></property>
    		<property name="student.name" value="学生C"></property>
    	</bean>
    ```

    

  - 外部已声明的bean的引用

    ```xml
    <bean id="student" class="com.spring.dev.dao.entity.Student">
    		<property name="name" value="学生A"></property>
    		<property name="age" value="12"></property>
    		<property name="gradeNo" value="13"></property>
    		<property name="classNo" value="23"></property>
    		<property name="schoolNo" value="23"></property>
    	</bean>
    	<bean id="person" class="com.spring.dev.dao.entity.Person">
    		<property name="name" value="张三"></property>
    		<property name="age" value="16"></property>
    		<property name="student" ref="student"></property>
    	</bean>
    ```

    

  - 内部bean

    ```xml
    <bean id="person" class="com.spring.dev.dao.entity.Person">
    		<property name="name" value="张三"></property>
    		<property name="age" value="16"></property>
    		<property name="student">
    			<bean class="com.spring.dev.dao.entity.Student">
    				<property name="name" value="学生B"></property>
    				<property name="age" value="12"></property>
    				<property name="gradeNo" value="13"></property>
    				<property name="classNo" value="23"></property>
    				<property name="schoolNo" value="23"></property>
    			</bean>
    		</property>
    	</bean>
    ```

    

##### 3、集合属性

​	在Spring中可以通过一组内置标签来配置集合属性，例如`<list>   <set>  <map>`

###### 	1. 数组和List

###### 	2. Map

###### 	3. 集合类型bean

```xml
	<!-- listAndMap -->
	<bean id="book01" class="com.spring.dev.dao.entity.Book">
		<property name="name" value="大学语文"></property>
	</bean>
	<bean id="book02" class="com.spring.dev.dao.entity.Book">
		<property name="name" value="大学数学"></property>
	</bean>
	<bean id="book03" class="com.spring.dev.dao.entity.Book">
		<property name="name" value="大学英语"></property>
	</bean>
	<bean id="student" class="com.spring.dev.dao.entity.Student">
		<property name="name" value="集合测试"></property>
		<property name="courseNames" ref="courseNames">
			<!-- <list>
				<value>语文</value>
				<value>数学</value>
				<value>英语</value>
			</list> -->
		</property>
		<property name="books" ref="books">
			<!-- <list>
				<ref bean="book01"/>
				<ref bean="book02"/>
				<ref bean="book03"/>
			</list> -->
		</property>
		<property name="courseBookMap">
			<map>
				<entry>
					<key>
						<value>大学语文</value>
					</key>
					<ref bean="book01"></ref>
				</entry>
				<entry>
					<key>
						<value>大学数学</value>
					</key>
					<ref bean="book02"></ref>
				</entry>
				<entry>
					<key>
						<value>大学英语</value>
					</key>
					<ref bean="book03"></ref>
				</entry>
			</map>
		</property>
	</bean>	
	<!-- 集合类型bean -->
	<util:list id="books">
		<ref bean="book01"/>
		<ref bean="book02"/>
		<ref bean="book03"/>
	</util:list>
	<util:list id="courseNames">
		<value>语文</value>
		<value>数学</value>
		<value>英语</value>
	</util:list>
```



##### 4、FactoryBean

​	Spring中有两种类型Bean，一种是普通的bean, 另一种是工厂bean,即FactoryBean

​	工厂bean跟普通的bean不同，工厂bean管理着普通bean，其返回的对象不是指定类的一个实例，其返回的是该工厂bean的getObject方法所返回的对象

​	工厂bean必须实现org.springFramework.beans.Factory.FactoryBean接口

​	

##### 5、bean的作用域

​		在Spring中可以通过`<bean>`元素的`scope`属性设置bean的作用域，来决定这个实例是单例还是多例

​		默认情况下，Spring只为每个在IOC容器里声明的bean创建唯一一个实例，整个IOC容器范围内都能共享该实例，所有后续的getBean()调用和bean引用都将返回这个唯一的bean实例，该作用称为`singleton`，它是所有bean的默认作用域

| 类别      | 说明                                                         |
| :-------- | ------------------------------------------------------------ |
| singleton | 在spring容器中仅存在一个实例，Bean以单实例存在               |
| prototype | 每次调用getBean()时都会返回一个新的实例                      |
| request   | 每次HTTP请求都会传创建一个新的Bean,该作用域仅适用于WebApplicationContext环境 |
| session   | 同一个HTTPSession共享一个Bean, 不同的HTTPSession使用不同的Bean,该作用域仅适用于WebApplicationContext环境 |

##### 6、bean的生命周期

- SpringIOC容器可以管理bean的生命周期，Spring允许bean生命周期内特定的时间点执行指定的任务

- SpringIOC容器对bean的生命周期进行管理的过程

  - 通过构造器或工厂方法创建bean实例
  - 为bean实例的属性设置值和其他bean的引用
  - 调用bean的初始化方法
  - 使用bean
  - 当容器关闭，调用bean的销毁方法

- 配置bean时，可以通过`init-method`和`destroy-method`属性为bean指定初始化和销毁方法

- **bean的后置处理器**

  - bean后置处理器允许在**调用初始化方法前后对bean进行额外的处理**

  - bean后置处理器**对IOC容器里的所有bean实例逐一处理，而非单一实例**

  - bean后置处理器需要实现接口

    `org.springframework.beans.factory.config.BeanPostProcessor`

    在初始化方法被调用前后，Spring将每个bean实例分别传递给上述接口的以下两个方法

    - `Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException;`
    - `Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException;`

  - **作用**：在Spring容器完成bean实例化、配置以及其他初始化方法前后要添加一些自己的逻辑处理时，我们可以定义一个或多个**BeanPostProcessor接口实现类**，然后注册到SpringIOC容器中

  - 定义多个BeanFactory接口实现类的执行顺序

- 添加bean后置处理器后bean的生命周期

  - 通过构造器或工厂方法创建bean实例
  - 为bean的属性设置值和对其他bean的引用
  - 将bean实例传递给后置处理器的postProcessBeforeInitialization()方法
  - 调用bean初始化方法
  - 将bean实例传递给后置处理器的postProcessAfterInitialization()方法
  - 使用bean
  - 当容器关闭时调用bean的销毁方法

##### 7、引用外部文件

- 在类路径下定义属性文件
- 使用标签导入文件
- 使用${keyname}获取值

```
<context:property-placeholder file-encoding="utf-8" location="classpath:init-data.properties"/>
<bean id="person" class="com.spring.dev.dao.entity.Person">
    <property name="name" value="${name}"></property>
    <property name="age" value="${age}"></property>
    <!-- <property name="name" value="dd"></property>
    <property name="age" value="45"></property> -->
</bean>
```

##### 8、自动装配

​	xml自动装配

​	注解自动装配



##### 9、通过注解使用bean

- 普通组件:  @Component

- 持久层:  @Repository

- 业务逻辑层: @Service

- 表述层控制器:  @Controller

- 组件命名规则

  - 默认驼峰命名，使用组件类名首字母小写得到的字符串作为bean的id
  - 使用组件注解的value属性指定bean的id

- 扫描组件

  ```xml
  <context:component-scan base-package="com.spring.dev"></context:component-scan>
  ```

  - base-package属性指定一个需要扫描的基类包，Spring容器将会扫描这个基类包以及其子包中的所有类
  - 当需要扫描多个包时可以使用逗号分隔
  - 如果仅希望扫描特定的类而非基包下所有类，可以使用resource-pattern属性过滤特定的类
  - 