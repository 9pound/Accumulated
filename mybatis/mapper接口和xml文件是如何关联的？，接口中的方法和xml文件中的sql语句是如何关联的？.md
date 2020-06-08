# mapper接口和xml文件是如何关联的？，接口中的方法和xml文件中的sql语句是如何关联的？



mapper接口和xml文件是如何关联的？

​	将xml 的namespace属性的值配置成接口的全限定名

```
<mapper namespace="com.school.mapper.AdvisorMapper">
</mapper>
```

接口中的方法和xml文件中的sql语句是如何关联的？

​	标签的ID属性和定义接口的方法名相同

```

```

接口中的方法可以重载（同名不同参）所以接口中的所有同名方法会对应着xml中同一个ID的方法