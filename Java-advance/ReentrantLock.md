# ReentrantLock

基本结构：

```
myLock.lock();
try {
	critical section
} finally {
	myLock.unlock();
}
```

它确保任何时刻只有一个线程进入临界区，一旦一个线程对象封锁了锁对象，其他任何线程都无法通过lock语句。当其他线程调用lock时，它们被阻塞，直到第一个对象释放所对象





**可重入**

​	线程可以重复的获得已经持有的锁，锁保持一个持有计数来跟踪lock方法的嵌套调用。

**条件变量**

- ​	条件变量则允许线程由于一些未达到的条件而阻塞。
- ​	管理那些获得了一个锁但是却不能做有用工作的线程

```
private Condition sufficientFunds;
while（account[from] < amount）{
	sufficientFunds.await();
}
```



**await （）** 

- 一旦一个线程调用await方法，它进入该条件的等待集，当锁可用时，该线程不能马上解除阻塞，相反，它处于阻塞状态，直到另一个线程调用同一个条件上的singnalAll（）方法为止
- 当一个线程调用await时它没有办法重新激活自身，将导致锁问题

**singnalAll（）**：通知等待的线程，此时有可能已经满足条件，值得再次去检测该条件

**singl（）：**随机解除等待集中某个线程的阻塞

