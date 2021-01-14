# Thread



start()

run()

currentThread()

sleep()

wait()

join()

yield()



interrupt：请求终止线程，将中断状态设置为true

interrupted：静态方法，检测当前线程是否被中断，清除该线程的中断状态，将中断状态设置为true

isInterrupted：检测当前线程是否被中断，不改变中断状态



getState()

setProivity()

setDaemon()



没有强制终止线程的方法（有一个stop但是过时了），

执行return语句返回

没有捕获异常时

