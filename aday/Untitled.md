#### 2020-06-09

一  java多线程高并发讲解

1、面试题

- 请描述synchronized和reentrantlock的底层实现及重入的底层原理

- 请描述锁的四种状态和升级过程

- CAS的ABA问题如何解决

- 请谈下AQS，为什么AQS的底层是CAS+volatile

- 请谈下你对volatile的理解

- volatile的可见性和禁止指令重排序是如何实现的

- CAS是什么

- 请描述下对象的创建过程

- 对象在内存中的布局

  Object实例在内存中的布局

  ![image-20200609085651686](F:\note\aday\Untitled\image-20200609085651686.png)

  

![image-20200609085724292](F:\note\aday\Untitled\image-20200609085724292.png)

markword     对象头部，8个字节, 包含synchronized等关键字

class pointer  对象头部的类指针，4个字节

instance data

padding   4个字节





- DCL单例为什么要加volatile

- 解释下锁的四种状态

- Object o = new Object()在内存中占了多少字节

  答：16 bytes

- 请描述synchronized和ReentrantLock的异同

- 聊聊你对as-if-serial和happens-before语义的理解

- 了解ThreadLocal吗，知道ThreadLocal中如何解决内存泄漏问题吗？

- 请描述下锁的分类以及在JDK中的应用

2、AtomicInteger

CAS (compare and swap) 比较交换，没有锁的情况下保证多个线程对一个值的更新

![image-20200609084124030](F:\note\aday\Untitled\image-20200609084124030.png)



synchronized

