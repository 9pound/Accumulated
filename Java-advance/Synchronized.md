# Synchronized

- java中每个对象都有一个内部锁，并且该锁只有一个内部条件。
- 如果一个方法用synchronized关键字生命，那么锁对象将保护整个方法

**原理：**



**wait（）**添加线程到等待集

**notify（）/notifyAll（）**解除等待线程的阻塞状态

****

**总结：**

- 锁用来保护代码片段，任何时刻只能有一个线程执行被保护的代码
- 锁可以管理试图进入被保护代码段的线程
- 锁可以拥有一个或多个条件
- 每个条件对象管理那些已经进入被保护的代码段但还不能运行的线程

#### synchronized 还有别的作用范围?

- 修饰实例方法

- 修饰静态方法

- 修饰代码块


#### synchronized的性质？

原子性

可重入性

#### synchronized是如何实现的，底层原理（monitorenter，monitorexits）？



#### synchronized 是公平锁还是非公平锁吗？

#### 双重校验锁实现单例模式

#### synchronized和Reentrantlock之间的区别？

#### 不使用synchronized如何实现一个线程安全的单例？

#### synchronized和原子性、可见性和有序性之间的关系？

#### Synchronized锁优化？

#### synchronized 锁状态怎么从无锁状态到偏向锁的吗？

#### 那你跟我讲讲偏向锁撤销怎么到轻量级锁的？

#### 还有轻量级锁什么时候会变成重量级锁？