# 动态SQL

<if>

<choose><when><otherwise>



<where> 

​	去除开头的AND和OR

<set>

​	去除结尾的逗号

<tirm>

​	去除开头和结尾的指定字符串

<foreach>

只有一个数组参数和集合参数的情况

```

<foreach collection="list" open="(" close=")" separator="," item="id" index=“i”>
	#{id}
</foreach>

<foreach collection="array" open="(" close=")" separator="," item="id" index=“i”>
	#{id}
</foreach>
```

参数是Map类型

```
将collection指定为对应map中的可以即可
```

