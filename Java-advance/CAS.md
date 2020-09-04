## CAS

CAS是一种乐观锁的实现、非阻塞的同步机制，CAS利用底层的原子机器指令代替锁来确保数据在并发访问中的一致性。它借助冲突检查机制来判断在更新的过程中是否存在来自其他线程的干扰。如果存在，这个操作将失败，并且可以重试，也可以不重试。





CAS包含3个操作数，需要读写得内存位置V、进行比较的值A和拟写入的新值B，当且仅当V值等于A时，CAS才会通过原子方式用新值B来更新V的值，否则不会执行任何操作，无论位置V的值是否等于A，都将返回V原有的值。（这种操作被称为比较并设置，无论操作是否成功都会返回）

CAS的含义是“我认为V的值，应该为A，如果是那么将V值更新为B，否则不修改并告诉V的实际值为多少

当多个CAS操作尝试使用CAS同时更新同一个变量时，只有其中一个线程能更新变量的值，而其他线程都将失败。失败的线程不会被挂起，而是被告知在这次竞争中失败，并可以再次尝试。



#### 锁的缺点

- 当一个线程在等待锁时，它不能做任何其他事情
- **优先级反转**（缺页从错误、调度延迟）那么所有需要这个锁的线程都无法执行下去
- 当在锁上存在着激烈的竞争时，调度开销与工作开销的比值会非常高

#### CAS的缺点

- CAS通过调用者处理竞争问题，而锁中能自动处理竞争问题（没有获得锁的线程将被阻塞）


**参考：**

https://blog.csdn.net/a314368439/article/details/82760982

https://blog.csdn.net/ls5718/article/details/52563959?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.edu_weight&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.edu_weight



多线程问题总结

https://www.cnblogs.com/Curry-Coder/p/6810785.html