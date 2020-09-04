oracle基本概念

**1、表空间？**

用于存放数据库表，索引，回滚段等对象的磁盘逻辑空间叫tablespace

![1554294338128](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\1554294338128.png)

**2、数据文件Datafile？**

oracle 数据库由表空间构成，每个表空间可以包含一个或者多个数据文件。表空间和数据文件是不可分割的数据库实体。本质上

总结如下

- 表空间是一个数据库的逻辑区；
- 每个表空间有一个或多个数据文件组成
- 一个数据文件只能属于一个表空间

**3、临时表空间(Temporary Tablespace)** 

存放与排序有关的特殊空间。相当于数据库中的一块白板，Oracle 将排序的数据临时存放在该表空间内，排序处理完后即可释放排序数据所占的空间

可以从数据字典DBA_TMP_FILE查询临时表空间的信息

​	select tablespace_name,file_name from dba_temp_files;

**4、数据字典**

数据字典是存放整个数据库实例重要信息的一组表

![1554347891405](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\1554347891405.png)

**5、存储结构**

**数据块：基本的处理单位，由操作系统块构成，有唯一标识**

段：占用空间的对象 表，索引，簇等，段由区间构成，区间由连续的数据块构成



# 常用命令

###### 1、删除USER。

 

DROP USER  CASCADE

 

2、删除表空间

 

DROP TABLESPACE tablespace_name INCLUDING CONTENTS AND DATAFILES;

 

删除空的表空间，不包含物理文件。

 

DROP TABLESPACE tablespace_name;

 

删除空表空间，包含物理文件。

 

DROP TABLESPACE tablespace_name INCLUDING DATAFILES;

 

删除 非空 表空间，不包含物理文件。

 

DROP TABLESPACE tablespace_name INCLUDING DATAFILES;

 

删除 非空 表空间，包含物理文件。

 

DROP TABLESPACE tablespace_name INCLUDING CONTENTS AND DATAFILES;

# 补充：（便于理解）

# [**mysql、orcl中database、schema、user之间的关系**](https://blog.csdn.net/nlznlz/article/details/63721693)

In MySQL:

- server instance == not identified with catalog, just a set of databases
- database == schema == catalog == a namespace within the server.
- user == named account, who can connect to server and use (but can not own - no concept of ownership) objects in one or more databases
- to identify any object you need (database name + object name)

In Oracle:

- server instance == database == catalog == all data managed by same execution engine
- schema == namespace within database, identical to user account
- user == schema owner == named account, identical to schema, who can connect to database, who owns the schema and use objects possibly in other schemas
- to identify any object you need (schema name + object name)