# Redis进阶

## 数据的持久化

也就是redis如何将数据存储到硬盘里？

### **快照**rdb

可以将存在于某一时刻的所有数据都写入硬盘里面

快照就是副本，创建快照就是创建存储在内存中的数据在某个时间点上的副本。

#### 创建快照的方法

**BGSAVE命令**

redis会调用fork命令来创建子进程，子进程将快照写入硬盘，而父进程则继续处理命令请求。

**SAVE命令**

redis服务器在快照创建完毕之前，不会响应任何其他命令

**通过SHUTDOWN关闭服务器或者接受到标准TERM型号时**

redis会执行一个SAVE命令，阻塞所有客户端不再执行客户端发出的任何命令，并在SAVE命令执行完毕之后关闭服务器。

**通过redis.conf配置文件，自动触发BGSAVE命令 **

save 60 10000

save 1    500

如果用户设置了多个save配置选项，那么当任意一个save配置选项所设置的条件被满足时，redis就会触发一次BGSAVE命令。

**SYNC命令**

当一台redis服务器连接另一台redis服务器，并向对方发送SYNC命令来开始一次复制操作的时候，如果主服务器目前没有在执行BGSAVE命令，或者主服务器并非刚刚执行完BGSAVE操作。那么主服务器就会执行BGSAVE命令。

#### **快照的缺点**

当redis存储的数据只有几个GB的时候，使用快照来保存数据是没有问题的

redis进程每占用一个GB，创建BGSAVE子进程所需要的时间就要 增加10~20毫秒 

## **只追加文件AOF**（append only file）

原理：在执行写命令时，将被执行的写命令复制到硬盘里面

**AOF的缺点**：AOF文件的体积大小

- 体积不断增大的AOF文件可能会用完硬盘的所有空。
- redis重启之后，需要通过重新执行AOF文件中的写命令来还原数据，如果AOF的体积非常大，那么还原操作的时间可能会非常长。

**如何解决AOF文件体积不断增大的问题**

- BGREWRITEAOF命令，该命令会移除通过移除AOF文件中的冗余命令来，重写AOF文件。redis会创建一个子进程然后由子进程负责对AOF文件进行重写。

### 补充

既可以同时使用，又可以单独使用，也可以都不使用

## 复制

复制可以让其他服务器拥有一个不断更新的数据副本，从而使得拥有数据副本的服务器，可以用于处理客户端发送的读请求，

关系数据库通常会使用一个主服务器向多个从服务器发送更新，并使用从服务器来处理所有读请求。 

#### REDIS主从服务器的配置方法



## Jedis API

#### Jedis 

Jedis jedis = new Jedis("192.168.25.27",6379);
		//jedis.auth(password);如果有 密码
		String value = jedis.get("mytest");
		System.out.println(value);
		jedis.close();

#### JedisPoolConfig

#### JedisPool

		JedisPoolConfig config = new JedisPoolConfig();
		config.setMaxIdle(8);
		config.setMaxTotal(18);
		JedisPool pool = new JedisPool(config,"192.168.25.27",6379,2000,"");
		Jedis jedis = pool.getResource();
		String value = jedis.get("mytest");
		
		System.out.println(value);
		
		jedis.close();
		pool.close();
#### Jedis Cluster

```
Set<HostAndPort> jedisClusterNodes = new HashSet<HostAndPort>();
//Jedis Cluster will attempt to discover cluster nodes automatically
jedisClusterNodes.add(new HostAndPort("127.0.0.1", 7379));
JedisCluster jc = new JedisCluster(jedisClusterNodes);
jc.set("foo", "bar");
String value = jc.get("foo");
```



#### 参考资料

https://github.com/xetorthio/jedis