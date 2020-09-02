# 接口中参数与Sql语句中的参数如何绑定

**参数类型**

- 基本类型
- JavaBean
- Map
- @Param注解

单参数

多个参数

在Sql语句中使用#{0}、#{2}、#{param1}、#{param2}

注解

```
List<User> selectUser(@param("userid") Long userId，@param（"enabled"）integer enabled);
```

