# 消息确认机制 （ message acknowledgement）



RabbitMQ 提供了消 息确认机制 （ message acknowledgement）。 消费者在订阅队列时，可以指定 autoAck 参数，当 autoAck 等于 false 时， RabbitMQ 会等待消费者显式地回复确认信号后才从内存 （或者磁盘）中移去消息（实质上 是先打上删除标记，之后再删除）。当 autoAck 等于 true 时， RabbitMQ 会自动把发送出去的 消息置为确认，然后从内存（或者磁盘）中删除，而不管消费者是否真正地消费到了这些消息。
采用消息确认机制后，只要设置 autoAck 参数为 false，消费者就有足够的时间处理消息 （任务〉，不用担心处理消息过程中消费者进程挂掉后消息丢失的问题， 因为 RabbitMQ 会一直 等待持有消息直到消费者显式调用 Basic.Ack 命令为止。



当 autoAck 参数置为 false，对于 RabbitMQ 服务端而言，队列中的消息分成了两个部分： 一部分是等待投递给消费者的消息： 一部分是己经投递给消费者，但是还没有收到消费者确认 信号的消息。如果 RabbitMQ 一直没有收到消费者的确认信号，并且消费此消息的消费者己经 断开连接，则 RabbitMQ 会安排该消息重新进入队列，等待投递给下一个消费者，当然也有可 能还是原来的那个消费者



“Ready”状态 和“Unacknowledged＂状态的消息数，分别对应上文中的等待投递给消费者的消息数和己经投 递给消费者但是未收到确认信号的消息数

RabbitMQ 不会为未确认的消息设置过期时间，它判断此消息是否需要重新投递给消费者的 唯一依据是消费该消息的消费者连接是否己经断开





在消费者接收到消息后，如果想明确拒绝当前的消息而不是确认，那么应该怎么做呢？ 



一次只能拒绝一条消息

 basicReject

，如果想要批量拒绝消息

 channel .basicNack 



Basic.Recover

用来请求 RabbitMQ 重新发送还未被确认的消息。 如 果 requeue 参数设置为 true，则未被确认的消息会被重新加入到队列中，这样对于同一条消息 来说，可能会被分配给与之前不同的消费者。如果 requeue 参数设置为 false，那么同一条消 息会被分配给与之前相同的消费者。默认情况下，如果不设置 requeue 这个参数，相当于 channel.basicRecover(true ），即 requeue 默认为 trueo