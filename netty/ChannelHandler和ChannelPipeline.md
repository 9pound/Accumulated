# ChannelHandler和ChannelPipeline



ChannelHandler的生命周期

handlerAdd

handlerRemoved

exceptionCaught

ChannelHandler的子接口

1. ChannelInBoundHandler：处理入站以及各种状态变化
2. ChannelOutBoundHandler：处理出站数据并且允许拦截所有操作





### ChannelInBoundHandler



### ChannelOutBoundHandler

​	处理出站操作和数据

​	可以按需推迟操作或者事件



### ResourceLeakDetector：检测内存泄漏

