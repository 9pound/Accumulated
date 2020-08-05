# Spring如何进行事务管理？

#### 编程式事务管理

在业务类中注入，事务管理模板类TransactionTemplate

```

```

#### 声明式事务管理

##### 原始的TransactionProxyFactoryBean

对业务类进行代理、并织入事务增强功能

##### 基于aop/tx命名空间配置



##### 使用注解配置声明式事务

@Transactional