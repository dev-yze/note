Redis

- 内存

- 工作线程单线程

- 键值对，有数据类型，数据类型本地方法

- 操作向数据流动

`Set`

场景：

​		推荐好友，交集，共同好友，差集推荐好友

集合、无序、不重复(去重)

```c
srandmember key count
参数条件
  1) count > 0
  	返回不重复的count个子元素(如果count > size, 返回全部元素)
  2) count < 0 and |count| < size
  	返回有可能重复的count个子元素
  3) count < 0 and |count| > size
	返回重复的count个子元素且些元素可能不会出现

// 求集合并集、交集、差集
sunion s1 s2
sinter s1 s2
sdiff k1 k2   // 求k1与k2的差集，返回k1差集
sdiff k2 k1   // 求k2与k1的差集，返回k2差集
```



`Sorted Set`

使用场景:

​		排行榜、有序事件、评论+分页(按时间、点赞数、动态分页(时间有增加、点赞数增加))

​		对于动态分页如评论，如果评论要按照条件进行分页而评论体积很大，可以将评论内容放到hash中，生成短小的键，再拿键按照不同的条件去生成sorted set，匹配时根据键查找到对应的内容

​		



优化：

redis具有5种Value类型，但存储值时每种类型可能有集中不同的数据结构

`ziplist`

`skiplist`





