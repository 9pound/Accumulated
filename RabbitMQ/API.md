# API

Connection 可以用来创建多个 Channel 实例，但是 Channel 实例不能在线程问共享， 应用程序应该为每一个线程开辟一个 Channel





#### exchangeDeclare 

```java
Exchange.DeclareOk exchangeDeclare(String exchange, String type, 
                                   boolean durable, boolean autoDelete, 
                                   boolean internal, Map<String, Ob] ect> arguments) throws IOException; 
```

- exchange： 交换器的名称。
- type： 交换器的类型，常见的如 fanout、 direct、 topic， 
- durable：设置是否持久化。 durable 设置为 true 表示持久化， 反之是非持久化。持 久化可以将交换器存盘，在服务器重启 的时候不会丢失相关信息
- autoDelete： 设置是否自动删除。 autoDelete 设置为 true 则表示自动删除。自动 删除的前提是至少有一个队列或者交换器与这个交换器绑定， 之后所有与这个交换器绑 定的队列或者交换器都与此解绑。注意不能错误地把这个参数理解为： “当与此交换器 连接的客户端都断开时， RabbitMQ 会自动删除本交换器”。
- internal： 设置是否是内置的。如果设置为 true，则表示是内置的交换器，客户端程 序无法直接发送消息到这个交换器中，只能通过交换器路由到交换器这种方式。
- argument： 其他一些结构化参数，比如 alternate-exchange 

exchangeDeclareNoWait 

exchangeDeclarePassive

它主要用来检测相应的交换器是否存在。如果 存在则正常返回：如果不存在则抛出异常： 404 channel exception，同时 Channel 也会被关闭。

exchangeDelet

exchangeDeleteNoWa







queueDeclare 

：队列的名称。
~ durable：设置是否持久化。为 true 则设置队列为持久化。持久化的队列会存盘，在 服务器重启的时候可以保证不丢失相关信息。
~ exclusive：设置是否排他。为 true 则设置队列为排他的。如果一个队列被声明为排 他队列，该队列仅对首次声明它的连接可见，并在连接断开时自动删除。这里需要注意 三点：排他队列是基于连接（Connection）可见的，同一个连接的不同信道（Channel) 是可以同时访问同一连接创建的排他队列：“首次”是指如果一个连接己经声明了一个 排他队列，其他连接是不允许建立同名的排他队列的，这个与普通队列不同：即使该队 列是持久化的，一旦连接关闭或者客户端退出，该排他队列都会被自动删除，这种队列 适用于一个客户端同时发送和读取消息的应用场景。
~ autoDelete：设置是否自动删除。为 true 则设置队列为自动删除。自动删除的前提是： 至少有一个消费者连接到这个队列，之后所有与这个队列连接的消费者都断开时，才会 自动删除。不能把这个参数错误地理解为：“当连接到此队列的所有客户端断开时，这 个队列自动删除”，因为生产者客户端创建这个队列，或者没有消费者客户端与这个队 列连接时，都不会自动删除这个队列。
~ arguments ：设置队列的其他一些参数，如 x-rnessage-ttl 、 x-expires 、 x-rnax-length、 x-rnax-length-bytes 、 x-dead-letter-exchange、 x-deadletter-routing-key, x-rnax-priority 等。





不带任何参数的 queueDeclare 方法默认创建一个由 RabbitMQ 命名的（类似这种 amq.gen-LhQzlgv3GhDOv8PIDabOXA 名称，这种队列也称之为匿名队列〉、排他的、自动删除 的、非持久化的队列。

queueDeclareNoWait

queueDeclarePass工ve 

。这个方法用来检测相 应的队列是否存在。 如果存在则正常返回，如果不存在则抛出异常： 404 channel exception，同 时 Channel 也会被关闭