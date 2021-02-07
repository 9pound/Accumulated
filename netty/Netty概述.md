# Netty概述

netty是一款异步的、事件驱动的、网络应用程序框架。用于快速开发高性能的网络应用程序

面向对象的基本概念：用简单的抽象隐藏底层实现的复杂性

异步：

事件驱动：

阻塞I/o

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

channel

回调

future

事件和ChannelHandler







阻塞和非阻塞网络操作之间的区别？

异步I/O 在高容量、高性能的网络编程中的优势？

netty的特点？

异步模型的底层机制？