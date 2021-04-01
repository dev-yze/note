

# `Redis`使用



- Redis是基于内存的存储数据库，绝大多数命令处理只是纯粹的内存操作，读写快
- Redis是单进程线程的服务（实际上一个正在运行的RedisServe肯定不止一个线程，但只有一个线程来处理网络请求）
- Redis使用多路I/O复用模型(select poll epoll), 可以高效处理大量并发连接
- Redis中的数据结构是专门设计的，增删改查等操作相对简单哪



## 安装配置

1、下载

2、安装



## 简介

- 数据库里面每个键值对都是由对象组成
  - 键总是一个字符串对象
  - 值可以是是字符串、哈希、list、set、zset、geo、hyperloglog中一种

## 数据类型

|      类型      | 描述 | 特性 | 场景 |
| :------------: | :--: | :--: | :--: |
| String(字符串) |      |      |      |
|Hash(哈希)||||
|List(列表)||||
|Set(集合)||||
|ZSet(有序集合)||||



#### String(字符串)

#### Hash(哈希)

#### List(列表)

#### Set(集合)

#### Zset(sorted set:有序集合)



## 高级数据类型

#### HyperLogLog

**描述:**	

- 做基数统计的算法

- 不存储输入元素本身，不能返回输入的各个元素
- 

**命令：**

- `pfadd  key1 value1 value2 ...`     		添加指定元素到HyperLogLog

- `pfcount key1`                                                 计返回基数估算值
- `pfmerge newkey key1 key2 ...`                将多个HyperLogLog合并为一个

```
dev_yze:0>pfadd hlkey01 aa bb cc dd
"1"
dev_yze:0>pf add h2key02 11 22 33 44 44 bb
"ERR unknown command `pf`, with args beginning with: `add`, `h2key02`, `11`, `22`, `33`, `44`, `44`, `bb`, "
dev_yze:0>pfadd h2key02 11 22 33 44 22 bb
"1"
dev_yze:0>pfmerge h3key03 h1key01 h2key02
"OK"
dev_yze:0>pfcount h3key03
"5"
dev_yze:0>
```



#### GEO

描述：

- 存储地理位置信息
- 操作存储的位置信息

命令:

- `geoadd key longitude latitude member [longitude latitude member ...]`

  存储指定地理空间

  longitude 经度

  latitude    纬度

  member  位置名称

  

- `geopos key member [member ...]`    从指定key里返回所有指定member

- `geodist key member01 member02 [m|km|mi|fi]`      计算两个位置之间的距离					                                     

  

- `georadius key longitude latitude radius m|km|mi|ft [WITHCOORD] [WITHDIST] [WITHHASH] [COUNT count] [ASC|DESC] [STORE key] [STOREDIST key]`

    返回以给定的经纬度为中心，返回键包含的位置元素中，与中心的距离不超过给定最大距离的所有位置元素



- `georadiusbymember key member radius m|km|mi|ft [WITHCOORD] [WITHDIST] [WITHHASH] [COUNT count] [ASC|DESC] [STORE key] [STOREDIST key]`

  以给定的位置元素为中心，找出指定范围内的元素

  - m 米
  - km
  - mi: 英里
  - ft: 英尺
  - widthdist: 返回位置元素同时，将位置元素与中心距离也一并返回
  - widthcoord: 将位置元素的经纬度一并返回
  - widthhash
  - count 限定返回的记录数
  - asc 查找结果从近到远排序
  - desc 从远到近排序

  

- `geohash key member [member ...]`                                          使用 geohash 来保存地理位置的坐标。

```
// 存位置信息
dev_yze:0>geoadd poList 13.444400 14.344434 "address01" 56.344444 59.233445 "address02"
"2"

dev_yze:0>geopos poList  address01
 1)    1)   "13.44439834356307983"
  2)   "14.34443441898374516"
// 取位置信息
dev_yze:0>geopos poList address01 address02
 1)    1)   "13.44439834356307983"
  2)   "14.34443441898374516"

 2)    1)   "56.34444326162338257"
  2)   "59.23344379014385197"
// 计算距离
dev_yze:0>geodist poList address01 address02  m
"6099157.2157"
dev_yze:0>geodist poList address01 address02 km
"6099.1572"

// 指定经纬度查找距离内位置元素
redis> GEOADD Sicily 13.361389 38.115556 "Palermo" 15.087269 37.502669 "Catania"
(integer) 2
redis> GEORADIUS Sicily 15 37 200 km WITHDIST
1) 1) "Palermo"
   2) "190.4424"
2) 1) "Catania"
   2) "56.4413"
redis> GEORADIUS Sicily 15 37 200 km WITHCOORD
1) 1) "Palermo"
   2) 1) "13.36138933897018433"
      2) "38.11555639549629859"
2) 1) "Catania"
   2) 1) "15.08726745843887329"
      2) "37.50266842333162032"
redis> GEORADIUS Sicily 15 37 200 km WITHDIST WITHCOORD
1) 1) "Palermo"
   2) "190.4424"
   3) 1) "13.36138933897018433"
      2) "38.11555639549629859"
2) 1) "Catania"
   2) "56.4413"
   3) 1) "15.08726745843887329"
      2) "37.50266842333162032"
redis>

// 指定位置名称查找距离内位置
```



## 发布订阅

Redis发布订阅(pub/sub)是一种消息通信模式：发送者(pub)发送消息，订阅者(sub)接收消息

Redis客户端可以订阅任意数量的频道

![img](E:\note\database\pubsub1.png)

client2、client5、client1订阅频道channel1

当有新消息通过publish命令发布给频道channel1时，这个消息会被发送给订阅它的三个客户端

![img](E:\note\database\pubsub2.png)



实例: 

```
client1创建并订阅频道
dev_yze:0>subscribe music
Switch to Pub/Sub mode. Close console tab to stop listen for messages.
 1)  "subscribe"
 2)  "music"
 3)  "1"

client2发布消息
dev_yze02:0>publish music "Hello World"
"1"
dev_yze02:0>publish music "逆战"
"1"
dev_yze02:0>

client1收到信息
dev_yze:0>subscribe music
Switch to Pub/Sub mode. Close console tab to stop listen for messages.
 1)  "subscribe"
 2)  "music"
 3)  "1"
 1)  "message"
 2)  "music"
 3)  "Hello World"
 1)  "message"
 2)  "music"
 3)  "逆战"
```



命令:

- `psubscribe pattern [pattern ...]` 				订阅一个或多个符合给定模式的频道
- `pubsub subcommand [argument[argument ...]]`      查看订阅发布系统状态
- `publish channel message`                                         将消息发布到频道上
- `subscribe channel [channel ...]`                               订阅给定的频道或多个频道的信息
- `unsubscribe channel [channel...]`                           退订给定的频道



## Redis Stream(流)

Redis Stream是Redis5.0新增加的数据结构

Redis Stream主要用于消息队列(MQ, Message Queue), Redis本事是有一个Redis发布订阅来实现消息队列功能，但有个缺点就是消息无法持久化，如果出现断网宕机，消息会被丢弃

Redis发布订阅分发消息，但无法记录历史消息

而Redis Stream提供了消息的持久化和主备复制功能，可以让任何客户端访问任何时刻的数据，并且能记住每一个客户端的访问位置，还能保证数据不丢失

Stream是Redis的数据类型中最复杂的，尽管数据类型本身很简单，它实现了额外的非强制性的特性；提供了一组允许消费者以阻塞



## 持久化

#### RDB持久化

#### AOF持久化



## 脚本



## 事务

Redis事务可以一次执行多个命令，并且有一下三个重要的保证

- 批处理操作在发送EXEC命令前被放入队列缓存
- 收到EXEC命令后进入事务执行，在事务任意命令执行失败，其余的命令依然被执行
- 在事务执行过程中，其它客户端提交的命令请求不会插入到事务执行命令中

一个事务从开始到执行经历一下三个阶段：

- 开始事务
- 命令入队
- 执行事务

单个Redis命令是原子性的，但Redis没有在事务上增加任何维持原子性的机制，所以Redis事务的执行不是原子性

命令：

- `discard`                           取消事务
- exec                                  执行事务块内所以命令
- multi                                 标记一个事务块开始
- unwatch                          取消watch命令对所有key的监视
- watch key [key ..]           监听一个或多个key，如果事务执行之前这个（或这些）key被其它命令所改动，那么事务将被打断

## 数据备份与恢复





# `Redis`源码



SDS

跳跃表

压缩列表

字典

整数集合

quicklist

Stream



持久化

主从复制

集群

