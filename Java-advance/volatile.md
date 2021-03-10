# volatile

#### Volatile变量不保证原子性

volatile关键字为实例域的同步访问提供了一种免锁机制。如果声明一个域为volatile，那么编译器和虚拟机就知道该域是可能被另一个线程并发更新

假设对共享变量除了赋值之外并不完成其他操作，那么可以将这些共享变量声明为volatile

#### volatile的底层原理

#### 缓存一致性协议

#### Java 内存模型



#### volatile读写规则

- 每次使用前都必须先从主内存中刷新最新的值
- 每次修改后都必须立刻同步会主内存中
- volatile修饰的变量不会被指令重排序优化





# FAQ

为什么要用 volatile 修饰？说说它的功能？

什么是 MESI 协议？CPU 原语是什么？

什么是可见性？

JMM 说说是什么？为什么要有 JMM？

[Happened-before](https://en.wikipedia.org/wiki/Happened-before) 是什么？它和 synchronized 的区别是什么？



