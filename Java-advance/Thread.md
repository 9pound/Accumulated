# Thread



start()：

run()：

currentThread()：

sleep()：

wait()：

join()：等待终止指定线程

yield()：使当前线程从执行状态（运行状态）变为可执行态，即使刚刚放弃了执行的权利, 也可能下一次就被调度回来了.



interrupt：用来请求终止线程，将中断状态设置为true

interrupted：静态方法，检测当前线程是否被中断，清除该线程的中断状态，将当前线程的中断状态重置为FALSE

isInterrupted：检测当前线程是否被中断，不改变中断状态



getState()

setProivity()

setDaemon()



没有强制终止线程的方法（有一个stop但是过时了），

执行return语句返回

没有捕获异常时



Thread.join() :当前线程A等待Thread线程终止之后才从thread.join()，返回



#### 阻塞与等待的区别？

被动阻塞没有获得锁，没有进入临界区

主动等待获得了锁，进入了临界区，暂时释放了锁
