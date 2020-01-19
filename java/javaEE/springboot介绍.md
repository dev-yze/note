一、Spring Boot简介

1、背景

​	Spring Framework是java/spring应用程序跨平台开发框架，也是JavaEE轻量框架，其Spring平台为Java开发者提供了全面的基础设施支持，虽然Spring基础组件代码是轻量级的，但其配置文件依旧是重量级的，因此产生了Spring Boot让开发Spring应用更简单

2、Spring Boot

Spring Boot框架是用于简化Spring应用从搭建到开发的过程。应用开箱即用，只要通过一个指令包括命令行 java -jar 、Spring Application应用启动类、Spring Boot Maven插件等，就可以启动应用，SpringBoot强调只需要很少的配置文件，所以在开发生产级Spring应用中，让开发变得更加高效和简易

3、Spring Boot WebFlux

​		大多数场景使用MVC都是阻塞式的，WebFlux使用的场景是异步非阻塞式的。

​		响应式编程：响应式编程是基于异步和时间驱动的非阻塞程序，只是垂直通过JVM内启动少量线程扩展，而不是水平通过集群扩展

​		Spring Boot 2.0包括一个新的Spring-webflux模块，该模块包含对响应式HTTP和WebSocket客户端的支持，以及对REST, HTML和websocket交互等程序的支持

