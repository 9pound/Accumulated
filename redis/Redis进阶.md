# Redis进阶



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