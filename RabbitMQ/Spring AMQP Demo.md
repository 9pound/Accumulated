# Spring AMQP Demo





```
@RabbitListener(bindings = @QueueBinding(
        value = @Queue(value = "leyou.delete.index.queue",durable="true"),
        exchange = @Exchange(
                value = "leyou.item.exchage",
                ignoreDeclarationExceptions = "true",
                type = ExchangeTypes.TOPIC
        ),
        key = "item.delete"
))
```

- `@Componet`：类上的注解，注册到Spring容器
- `@RabbitListener`：方法上的注解，声明这个方法是一个消费者方法，需要指定下面的属性：
  - `bindings`：指定绑定关系，可以有多个。值是`@QueueBinding`的数组。`@QueueBinding`包含下面属性：
    - `value`：这个消费者关联的队列。值是`@Queue`，代表一个队列
    - `exchange`：队列所绑定的交换机，值是`@Exchange`类型
    - `key`：队列和交换机绑定的`RoutingKey`