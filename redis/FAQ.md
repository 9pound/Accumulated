# FAQ

#### 九大数据结构

- string
- list
- set
- zset
- hash
- stream
- bitmap
- hyperloglogs
- geo

#### 事务（五个指令）

#### 持久化

- rdb
- aof

#### 键过期(两种)

#### 内存淘汰策略（六种）

#### 分布式锁

- setnx
- redlock

#### 延时队列

- list
- pub/sub

#### 发布订阅

#### 双写一致性(三种策略)

#### 缓存穿透、缓存击穿、缓存雪崩

#### Redis线程模型

#### 高可用（主从、哨兵、集群）

主从同步机制

集群策略







1. 是什么？与memcached有什么区别？
2. Redis的五种数据结构(STRING、LIST、SET、HASH、ZSET)及常用命令
3. 一个字符串类型的值能存储最大容量是多少？512M
4. Redis的事务特性和流水线特性  
5. Redis 是单进程单线程的？
6. redis 过期键的删除策略？
7. Redis 的回收策略（淘汰策略）?
8. Redis key 的过期时间和永久有效分别怎么设置？
9. Redis如何做持久化的？快照、只追加文件
10. Redis的同步机制了解么？主从复制特性（避免对主服务器进行集中式访问）
11. 同时使用复制和持久化的好处和坏处？如何去选择适合自己的持久化选项和复制选项？
12. 使用过 Redis 做异步队列么，你是怎么用的？
13. 使用过Redis分布式锁么，它是什么回事？
14. 维护数据安全以及应对系统故障的方法？
15. 假如 Redis 里面有 1 亿个 key，其中有 10w 个 key 是以某个固定的已知的前缀开头的，如果将它们全部找出来？
16. 如果有大量的 key 需要设置同一时间过期，一般需要注意什么？
17. 发布订阅？
18. 分布式锁如何实现
19. 缓存穿透、缓存







[参考](https://blog.csdn.net/Design407/article/details/103242874?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight)

![image-20210824010105960](E:\Accumulate\redis\FAQ.assets\image-20210824010105960.png)

![image-20210824010855692](E:\Accumulate\redis\FAQ.assets\image-20210824010855692.png)

![image-20210824010921722](E:\Accumulate\redis\FAQ.assets\image-20210824010921722.png)

![image-20210824010938568](E:\Accumulate\redis\FAQ.assets\image-20210824010938568.png)

![image-20210824011013912](E:\Accumulate\redis\FAQ.assets\image-20210824011013912.png)