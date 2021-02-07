# Netty概述

netty是一款异步的、事件驱动的、网络应用程序框架。用于快速开发高性能的网络应用程序

面向对象的基本概念：用简单的抽象隐藏底层实现的复杂性

**异步**：异步方法会立即返回，并且在它完成时，会直接或者在稍后的某个时间点通知用户

**非阻塞网络**：不必等待一个操作的完成

**事件驱动**：

**选择器**：使得我们可以通过较少的线程便可监视许多连接上的事件

**一个既是异步又是事件驱动的系统**：可以以任意的顺序响应任意的时间点产生的事件、

**阻塞I/o例子：**

```
ServerSocket serverSocket = new ServerSocket(portNum);
Socket clientSocket = serverSocket.accept();
BufferedReader in = new BufferedReader(new InputStreamrReader(clientSocket.getInputStream));
PrintWriter out = new PrintWriter(clientSocket.getOutputStream,true);
String request,response;
while((request = in.readLine()) != null)
{
	if("Done".equals(request)){
		break;
	}
	response = processRequest(request);
	out.println(response);
}

```

## 核心组件

**Channel：**

- NIO 的基本构造块：代表一个到实体的开放连接（传入或者传出数据的载体）

**回调：**

- 一个回调其实就是一个方法，一个指向已经被提供给另外一个方法的方法引用。这使得后者可以在适当的时候调用前者，
- netty内部使用回调来处理事件，当一个回调被触发时，相关的事件可以被一个interface-ChannelHandler的实现处理

**Future** 回调和Future是相互补充的机制

- future提供了另一种在操作完成时通知应用程序的方式，这个对象可以看做是一个异步操作的结果的占位符，它将在未来的某个时刻完成，并提供对其结果的访问（缺点：只允许手动检查对应的操作是否完成，或者一直阻塞直到它完成）
- ChannelFuture：
- ChannelFutureListenner:提供通知机制，消除了手动检查对应的操作是否完成的必要（可以看做是回调的一个精细版本）

```
Channel channel = ...;
ChannelFuture future = channel.connect(new InetSocketAddress("192.168.0.1",25));
future.addListener(new ChannelFutureListenner() {
	@Override
	public void operationComplete(ChannelFutrue future) {
		if (future.isSuccess()){
			ByteBuf buffer = Unpooled.copiedBuffer("Hello",Charset.defaultCharset());
			ChannelFuture wf = future.chanel().writeAndFlush(buffer);
		} else {
			Throwable cause = future.cause();
			cause.printStackTrace();
		}
	}
});
```

**事件和ChannelHandler**

- ​	每个事件都可以被分发个ChannelHandler类中某个用户实现的方法
- ​	每个ChannelHandler的实例都类似于一种为了响应特定事件而被执行的回调









阻塞和非阻塞网络操作之间的区别？

异步I/O 在高容量、高性能的网络编程中的优势？

netty的特点？

异步模型的底层机制？