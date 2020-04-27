RocketMQ4

ActiveMQ

Kafka

解析mysqlBinlog

### 一、JMS（Java Message Service）

1、什么是JMS

2、

3、使用场景

- 核心应用
  - 解耦
  - 异步
  - 削峰
- 跨平台、多语言
- 分布式事务、最终一致性
- RPC调用上下游对接，数据源变动-》通知下属

4、AMQP协议

​		amqp协议是具有现代特征的二进制协议，是一个提供统一消息服务的应用层标准高级消息队列协议，是应用层协议的一个开发标准，为面向消息的中间件设计

​		Server:  接收客户端的连接，实现AMQ实体服务

​		Connection: 连接,应用程序与Server的网络连接，TCP连接

​		Channel:  信道，消息读写操作在信道中进行，客户端可以建立多个信道，每个信道代表一个会话任务.

​		Message:  消息,应用程序和服务器之间传送的数据，可以很简单，也可以很复杂,有Properties和Body组成，Properties为外包装，可以对消息进行修饰，比如消息的优先级、延迟等高级特性，Body就是消息主体

​		Virtual Host:  虚拟主机,用于逻辑隔离。一个虚拟主机里面可以有若干个Exchange和Queue,同一个虚拟主机里面不能有相同名称的exchange或Queue

​		Exchange:  交换器,接收消息，按照路由规则将消息路由到一个或者多个队列，如果路由不到，或者返回给生产者，或者直接丢弃

​		Binding: 绑定，交换器和消息队列之间的虚拟连接，绑定中可以包含一个或者多个RoutingKey

​		RoutingKey:  路由键,生产者将消息发送给交换器的时候，会发送一个RoutingKey,用来指定路由规则，这样交换器就知道把消息发送给哪个队列，路由键通常为一个“.”分割的字符串,例如”com.rabbitmq”

​		Queue:  消息队列，用来保存消息，供消费者消费

### 二、消息中间件常见概念和编程模型



1、常见概念

- JMS提供者
- JMS生产者
- JMS消费者
- JMS消息
- JMS队列
- JMS主题
- JMS消息模型

2、基础编程模型

- MQ中需要用的一些类
- ConnectionFactory ：连接工厂，JMS用它来创建连接
- Connection ：JMS客户端到JMS Provider的连接
- Session：一个发送或接收消息的线程
- Destination：消息的目的地；消息发给谁
- MessageConsumer / MessageProducer：消息消费者，消息生产者

![](F:\note\java\Untitled 1\WechatIMG2.png)

​	

### 三、主流消息队列和技术选型讲解

### 四、RocketMQ

#### （一）概述

#### （二）架构

#### （三）使用

##### 	1、配置RocketMQ服务器，启动名称服务和broker

​		在linux或者windows安装RocketMQ,启动mqnameser，启动mqbroker

##### 	2、生产者和消费者开发

###### 		（1）引入依赖

```xml
<properties>
    <java.version>1.8</java.version>
    <rocketmq.version>4.1.0-incubating</rocketmq.version>
</properties>
<dependency>
    <groupId>org.apache.rocketmq</groupId>
    <artifactId>rocketmq-client</artifactId>
    <version>${rocketmq.version}</version>
</dependency>
<dependency>
    <groupId>org.apache.rocketmq</groupId>
    <artifactId>rocketmq-common</artifactId>
    <version>${rocketmq.version}</version>
</dependency>
```

###### 		（2）配置RocketMQ服务器相关信息

```java
# 消费者的组名
apache.rocketmq.consumer.PushConsumer=orderConsumer
# 生产者的组名
apache.rocketmq.producer.producerGroup=Producer
# NameServer地址
apache.rocketmq.namesrvAddr=127.0.0.1:9876
```

###### 		（3）创建生产者生产

```java
package com.learn.rocketmq.jms;
import org.apache.rocketmq.client.producer.DefaultMQProducer;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;
import javax.annotation.PostConstruct;

@Component
public class MsgProducer {
    /**
     * 生产者的组名
     */
    @Value("${apache.rocketmq.producer.producerGroup}")
    private String producerGroup;
    /**
     * NameServer 地址
     */
    @Value("${apache.rocketmq.namesrvAddr}")
    private String namesrvAddr;
    /**
     * 生产者
     */
    private DefaultMQProducer producer ;
    public DefaultMQProducer getProducer(){
        return this.producer;
    }
    /**
     * 启动初始化
     */
    @PostConstruct
    public void defaultMQProducer() {
        //生产者的组名
        producer = new DefaultMQProducer(producerGroup);
        //指定NameServer地址，多个地址以 ; 隔开
        //如 producer.setNamesrvAddr("192.168.100.141:9876;192.168.100.142:9876;192.168.100.149:9876");
        producer.setNamesrvAddr(namesrvAddr);
        producer.setVipChannelEnabled(false);
        try {
            /**
             * Producer对象在使用之前必须要调用start初始化，只能初始化一次
             */
            producer.start();

        } catch (Exception e) {
            e.printStackTrace();
        }
        // producer.shutdown();  一般在应用上下文，关闭的时候进行关闭，用上下文监听器
    }
}
```

###### 		（4）创建消费者

```java
package com.learn.rocketmq.jms;

import org.apache.rocketmq.client.consumer.DefaultMQPushConsumer;
import org.apache.rocketmq.client.consumer.listener.ConsumeConcurrentlyStatus;
import org.apache.rocketmq.client.consumer.listener.MessageListenerConcurrently;
import org.apache.rocketmq.client.consumer.listener.MessageListenerOrderly;
import org.apache.rocketmq.common.consumer.ConsumeFromWhere;
import org.apache.rocketmq.common.message.MessageExt;
import org.apache.rocketmq.remoting.common.RemotingHelper;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

import javax.annotation.PostConstruct;
import java.util.SplittableRandom;

/**
 * @author zhangen.yang
 * @date 2020/4/23
 */
@Component
public class MsgConsumer {

    @Value("${apache.rocketmq.consumer.PushConsumer}")
    private String consumerGruop;

    @Value("${apache.rocketmq.namesrvAddr}")
    private String namesrvAddr;

    private DefaultMQPushConsumer pushConsumer;

    @PostConstruct
    public void defaultMQPushConsumer() {
        // 设置消费者组
        pushConsumer = new DefaultMQPushConsumer(consumerGruop);
        // 设置名称服务
        pushConsumer.setNamesrvAddr(namesrvAddr);
        try {
            //设置订阅的topic和tag, *表示全部tag
            pushConsumer.subscribe("testTopic", "*");
            // ConsumeFromWhere.CONSUME_FROM_LAST_OFFSET 默认策略，从该列最尾开始消费
            // ConsumeFromWhere.CONSUME_FROM_TIMESTAMP
            // ConsumeFromWhere.CONSUME_FROM_FIRST_OFFSET 从队列最开始消费
            pushConsumer.setConsumeFromWhere(ConsumeFromWhere.CONSUME_FROM_FIRST_OFFSET);

            // 消费者注册监听器
            // MessageListenerOrderly 有序的
            //MessageListenerConcurrently 处理消息无序，并行的方式处理，效率高
            pushConsumer.registerMessageListener((MessageListenerConcurrently) (list, context) -> {
                try {
                    for (MessageExt messageExt : list) {
                        System.out.println("messageExt: " + messageExt); // 输出消息内容
                        String messageBody = new String(messageExt.getBody(), RemotingHelper.DEFAULT_CHARSET);
                        System.out.println("消费者响应: msgId : " + messageExt.getMsgId() + ", msgBody : " + messageBody);
                    }
                } catch (Exception e) {
                    e.printStackTrace();
                    return ConsumeConcurrentlyStatus.RECONSUME_LATER; // 稍后再试
                }
                return ConsumeConcurrentlyStatus.CONSUME_SUCCESS; // 消费成功
            });
            pushConsumer.start();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

###### 		（5）测试

```java
import com.learn.rocketmq.jms.MsgProducer;
import org.apache.rocketmq.client.exception.MQBrokerException;
import org.apache.rocketmq.client.exception.MQClientException;
import org.apache.rocketmq.client.producer.SendResult;
import org.apache.rocketmq.common.message.Message;
import org.apache.rocketmq.remoting.common.RemotingHelper;
import org.apache.rocketmq.remoting.exception.RemotingException;
@RestController
@RequestMapping("/api/v1")
public class OrderController {
    @Autowired
    private MsgProducer msgProducer;
    @GetMapping("order")
    public CommonResult order(String topic, String msg, String tag) throws UnsupportedEncodingException, InterruptedException, RemotingException, MQClientException, MQBrokerException {
        Message message = new Message("testTopic", tag, msg.getBytes(RemotingHelper.DEFAULT_CHARSET));
        SendResult sendResult = msgProducer.getProducer().send(message);
        System.out.println("发送响应: MsgId:" + sendResult.getMsgId() + ", 发送状态: " +sendResult.getSendStatus());
        return CommonResult.ok();
    }
}
```



### 五、ActiveMQ

#### （一）概述

#### （二）架构

#### （三）使用

##### 	1、点对点消息

```
<!-- 加入依赖 -->
<!-- activemq -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-activemq</artifactId>
</dependency>
<!-- activemq-pool -->
<dependency>
    <groupId>org.apache.activemq</groupId>
    <artifactId>activemq-pool</artifactId>
</dependency>
<dependency>
    <groupId>org.messaginghub</groupId>
    <artifactId>pooled-jms</artifactId>
    <version>1.0.3</version>
</dependency>
```

​	2、application.properties配置

```
# broker服务器
spring.activemq.broker-url=tcp://121.199.37.169:61616/
#集群配置
#spring.activemq.broker-url=failover:(tcp://localhost:61616,tcp://localhost:61617)
spring.activemq.user=admin
spring.activemq.password=admin
# 线程池配置
spring.activemq.pool.enabled=true
spring.activemq.pool.max-connections=100
```

3、启动加注解@EnableJms

4、生产者

```java
import com.learn.activemq.service.ProducerService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jms.core.JmsMessagingTemplate;
import org.springframework.stereotype.Service;
import javax.jms.Destination;
import javax.jms.Queue;
/**
 * 消息生产者
 * @author zhangen.yang
 * @date 2020/4/23
 */
@Service
public class ProducerServiceImpl implements ProducerService {
    @Autowired
    private JmsMessagingTemplate jmsMessagingTemplate;  // 用来发送消息到broker的对象
    @Autowired
    private Queue queue;
    /**
     * 指定消息队列和消息
     * @param destination  发送到的消息队列
     * @param message 等待发送的消息
     */
    @Override
    public void sendMessage(Destination destination, String message) {
        jmsMessagingTemplate.convertAndSend(destination, message);
    }
    /**
     * 使用默认消息队列发送消息
     * @param message
     */
    @Override
    public void sendMessage(String message) {
        jmsMessagingTemplate.convertAndSend(this.queue, message);
    }
}

```

5、消费者监听队列

```java
package com.learn.activemq.jms;
import org.springframework.jms.annotation.JmsListener;
import org.springframework.stereotype.Component;
/**
 * @author zhangen.yang
 * @date 2020/4/23
 */
@Component
public class OrderConsumer {
    @JmsListener(destination = "order.queue")
    public void reciveQueue(String txt) {
        System.out.println("OrderConsumer收到报文为: " + txt);
    }
}
```

6、测试

```java
package com.learn.activemq.controller;
import com.learn.activemq.service.ProducerService;
import com.learn.apicommon.model.CommonResult;
import org.apache.activemq.command.ActiveMQQueue;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import javax.jms.Destination;
/**
 * @author zhangen.yang
 * @date 2020/4/23
 */
@RestController
@RequestMapping("/api/active-mq")
public class OrderController {
    @Autowired
    private ProducerService producerService;
    @GetMapping("order")
    public Object order(String msg) {
        Destination destination = new ActiveMQQueue("order.queue");
        producerService.sendMessage(destination, msg);
        return CommonResult.ok();
    }
    @GetMapping("common")
    public Object common(String msg) {
        producerService.sendMessage(msg);
        return CommonResult.ok();
    }
}
```

##### 2、订阅和点对点

(1) 配置文件修改，开启订阅模型

```
#default point to point
spring.jms.pub-sub-domain=true
```

(2) 建立订阅主题bean

```java
/**
 * 订阅主题
 * @return
 */
@Bean("videoTopic")
public Topic topic() {
    return new ActiveMQTopic("video.topic");
}
```

(3) 生产者发布主题消息

```java
@Service
public class ProducerServiceImpl implements ProducerService {

    @Autowired
    private JmsMessagingTemplate jmsMessagingTemplate;  // 用来发送消息到broker的对象

    @Autowired
    private Queue queue;

    /**
     * 发布的主题
     */
    @Autowired
    private Topic videoTopic;

    /**
     * 指定消息队列和消息
     * @param destination  发送到的消息队列
     * @param message 等待发送的消息
     */
    @Override
    public void sendMessage(Destination destination, String message) {
        jmsMessagingTemplate.convertAndSend(destination, message);
    }

    /**
     * 使用默认消息队列发送消息
     */
    @Override
    public void sendMessage(String message) {
        jmsMessagingTemplate.convertAndSend(this.queue, message);
    }

    /**
     * 主题发布
     */
    public void publish(String msg) {
        jmsMessagingTemplate.convertAndSend(this.videoTopic, msg);
    }
}
```

(4) 消费者监听主题

消费者1：

```java
@Component
public class CommonConsumer {
    @JmsListener(destination = "common.queue")
    public void reciveQueue(String txt) {
        System.out.println("OrderConsumer收到报文为: " + txt);
    }
    @JmsListener(destination = "video.topic")
    public void subscriptionTopic(String msg) {
        System.out.println("CommonConsumer订阅主题video.topic的推送为: "  + msg);
    }
}
```

消费者2：

```java
@Component
public class OrderConsumer {
    @JmsListener(destination = "order.queue")
    public void reciveQueue(String txt) {
        System.out.println("OrderConsumer收到报文为: " + txt);
    }
    @JmsListener(destination = "video.topic")
    public void subscriptionTopic(String msg) {
        System.out.println("OrderConsumer订阅主题video.topic的推送为: " + msg);
    }
}
```

（5）测试

```java
*******打印结果***********
OrderConsumer订阅主题video.topic的推送为: 测试呵呵order
CommonConsumer订阅主题video.topic的推送为: 测试呵呵order
```

### 六、Kafaka





### 七、RabbitMQ

(一)  概述

​	1、是什么

​	2、核心概念

AMQP协议



(二)



(三)

