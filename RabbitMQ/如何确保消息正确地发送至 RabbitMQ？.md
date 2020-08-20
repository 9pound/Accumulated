# 如何确保消息正确地发送至 RabbitMQ？ 如何确保消息接收方消费了消息？

- 通过事务机制实现
- 令通过发送方确认（publisher confirm）机制实现。

#### 传输保障分为三个层级。

- At most once：最多一次。消息可能会丢失，但绝不会重复传输。
- At least once：最少一次。消息绝不会丢失，但可能会重复传输。
- Exactly once：恰好一次。每条消息肯定会被传输一次且仅传输一次。

#### 事务机制

channel . txCommit 提交事务， 

channel.txRollback 事务回滚。

channel.txSelect 开启事务





![image-20200820173958447](C:\Users\shazi\AppData\Roaming\Typora\typora-user-images\image-20200820173958447.png)

1. 客户端发送 Tx.Select，将信道置为事务模式；
2. Broker 回复 Tx . Select-Ok，确认己将信道置为事务模式：
3. 令在发送完消息之后，客户端发送 Tx . Commit 提交事务
4. Broker 回复 Tx.Commit-Ok，确认事务提交。

#### 发送方确认

事务会使发送端阻塞、发送方确认机制是异步的

过程

1、信道设置成 confirm （确认）模式（ channel . confirmSelect ），在该信道上发送的消息都会被指派一个唯一的 ID 

2、投递到所有匹配的队列之后， RabbitMQ 就会发送一个确认（Basic.Ack）给生产者（包含消息的唯一 ID）

3、如果 RabbitMQ 因为自身内部错 误导致消息丢失，就会发送一条 nack (Basic . Nack）命令，生产者应用程序同样可以在回调 方法中处理该 nack 命令。



#### 接受方确认

**消费模式分两种**： 

- 推（Push）模式，推模式采用 Basic . Consume 进行消费。
- 拉（Pull）模式，而拉模式则是调用 Basic . Get 进行消费。



Basic . Consume 将信道（ Channel ）直为接收模式，直到取消队列的订阅为止。在接收模式期间，RabbitMQ 会不断地推送消息给消费者，当然推送消息的个数还是会受到 Basic.Qos 的限制、如果要实现高吞吐量，消费者理应使用 Basic.Consume 方法。

如果只想从队列获得单条消息而不是持续订阅，建议还是使用 Basic.Get 进行消费．但是不能将 Basic.Get 放在一个循环里来代替 Basic.Consume，这样做会严重影响 RabbitMQ 的性能．



#### **消息确认机制**

消费者在订阅队列时，可以指定 autoAck 参数，当 autoAck 等于 false 时， RabbitMQ 会等待消费者显式地回复确认信号后才从内存 （或者磁盘）中移去消息（实质上 是先打上删除标记，之后再删除）。当 autoAck 等于 true 时， RabbitMQ 会自动把发送出去的 消息置为确认，然后从内存（或者磁盘）中删除，而不管消费者是否真正地消费到了这些消息。

当 autoAck 参数置为 false，对于 RabbitMQ 服务端而言，队列中的消息分成了两个部分： 一部分是等待投递给消费者的消息： 一部分是己经投递给消费者，但是还没有收到消费者确认 信号的消息。如果 RabbitMQ 一直没有收到消费者的确认信号，并且消费此消息的消费者己经 断开连接，则 RabbitMQ 会安排该消息重新进入队列，等待投递给下一个消费者，当然也有可 能还是原来的那个消费者。

RabbitMQ 不会为未确认的消息设置过期时间，它判断此消息是否需要重新投递给消费者的 唯一依据是消费该消息的消费者连接是否己经断开，这么设计的原因是 RabbitMQ 允许消费者 消费一条消息的时间可以很久很久。