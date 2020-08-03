# Mybatis 常用注解

注解方式，可以将sql语句直接写在接口上，缺点是，当sql语句变化时都需要重新编译代码。

@Select

```java
@Select("{select id,role_name from sys_role where id = #{id}}")
SysRole selectById(Long id);
```

@Insert  @Option @SelectKey

```java
@Insert(insert into sys_role(role_name,...,create_time) values(#{roleName},...,#{createTime,jdbcType=TIMESTAMP}))
@Option(userGenerateedKeys = true,keyProperty = "id")
int insert1(SysRole sysRole)

@Insert(insert into sys_role(role_name,...,create_time) values(#{roleName},...,#{createTime,jdbcType=TIMESTAMP}))
@SelectKey(statement = "select LAST_INSERT_ID()"),
			keyProperty = "id",
			resultType = Long.class,
			before = fasle)
int insert2(SysRole sysRole)


```

@Update

@Delete



@Results 

```java
@Results(
id="roleResultMap",
valu={
	@Result(property = "id",column = "id",id = "true"),
	@Result(property = "roleName",column = "role_name"),
	...
}		
)
@Select("{select id,role_name from sys_role where id = #{id}}")
SysRole selectById2(Long id)


```

@ResultMap 可以通过ID 属性引用 @Results定义的映射关系

```java
@ResultMap("roleReslutMap")
@Select("{select * from sys_role}")
SysRole getAllRole();
```





@SelectProvider 

```java
@SelectProvider(type=PrivilegeProvider.class,method="selectById")
SysPrivilege selectById(Long id)
```

@InsertProvider

@UpdateProvider

@DeleteProvider

