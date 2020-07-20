# CAP和BASE理论

分布式事务：由多个分布式操作序列组成

C（Consistency）：一致性、

A（Availability）：可用性

P（Partition tolerance）： 分区容错性



CAP：一个分布式系统不可能同时满足C、A、P、最多只能同时满足其中的两项





# Base理论

​	Basically Available （基本可用）、Sof state（软状态）、Eventually consistent(最终一致性)



软状态：允许系统在不同节点的数据副本之间进行数据同步的过程存在延时。

核心思想：即使无法做到强一致性，但每个应用都可以根据自身的业务特点，采用适当的方式来使系统达到最终一致性



最终一致性的五个变种

因果一致性（Causal consistency）：

读己之所写（Read your write）（特殊的因果一致性）：

会话一致性（Session consistency）：系统能保证在同一个有效的回话中实现“读己之所写”的一致性，也就是说，执行更新操作之后，客户端能够在同一个回话中始终读取到该数据项的最新值

单调读一致性（Monotonic read consistency）：如果一个进程读取出一个数据项的某个值后、那么系统对于该进程后续的任何数据访问都不应该返回旧值

单调写一致性（Monotonic write consistency）:一个系统需要能够保证来自同一个进程的写操作被顺序的执行