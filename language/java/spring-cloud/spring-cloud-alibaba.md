alibaba blob: https://github.com/alibaba/spring-cloud-alibaba/blob/master/README-zh.md

spring cloud alibaba提供：

​		



### 一、Nacos

#### 1、概述

关键特性：

- 服务发现和服务健康检测
- 动态配置服务
- 动态DNS服务
- 服务及其元数据管理



#### 2、安装

```
windows安装
	cmd startup.cmd  //启动
	cmd shutdown.cmd //关闭
linux安装
	cd nacos/bin
	sh startup.sh -m standalone           // standalone代表单机模式
	bash startup.sh -m standalone		  // ubuntu,可以尝试如此
	
	sh shutdown.sh
```



#### 4、服务注册&发现和配置管理

```
服务注册: 向nacos注册服务，参数有服务名称、ip、端口号
	curl -X POST 'http://127.0.0.1:8848/nacos/v1/ns/instance?serviceName=nacos.nameing.serviceName&ip=20.18.7.10&port=8080'
	分析：
	  uri: http://127.0.0.1:8848/nacos/v1/ns/instance
	 参数：
	 	serviceName: 注册服务名称
	 			 ip: 注册服务ip
               port: 注册服务端口号

服务发现: 根据服务名称获取服务实例集群
	curl -X GET 'http://127.0.0.1:8848/nacos/v1/ns/instance/list?serviceName=nacos.naming.serviceName'
	分析：
	  uri: http://127.0.0.1:8848/nacos/v1/ns/instance/list
	参数:
	  serviceName: 提供者服务名称
	
发布配置: 向服务修改或发布配置，根据dataId,group确定content
	curl -X POST "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test&content=HelloWorld"
	分析:
	  uri: http://127.0.0.1:8848/nacos/v1/cs/configs
	参数: 
	   dataId:
	    group:
	  content:

获取配置: 根据dataId和group向服务获取配置数据
	curl -X GET "http://127.0.0.1:8848/nacos/v1/cs/configs?dataId=nacos.cfg.dataId&group=test"
	分析:
	 uri: http://127.0.0.1:8848/nacos/v1/cs/configs
	 参数: 
	 	dataId
	 	group
```



5、SpringCloud整合Nacos

1、服务注册与发现

2、配置中心



### 二、Sentinel

流量控制、熔断降级、系统负载保护



整合feign

​	添加依赖

​	修改配置文件

​	启动类开启注解@EnableFeignClients