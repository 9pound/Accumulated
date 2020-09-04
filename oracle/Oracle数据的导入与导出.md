# Oracle数据的导入与导出

## 1、方法两种

- imp/exp客户端程序
- impdp/expdp数据泵

## **2、什么是数据泵（data pump）？**

数据泵是一种在数据库之间，或者，在数据库与操作系统之间传输数据或元数据的高速机制。

### **特点**

- 目录路径上载和直接路径装入

- 运行在服务器上

- 断点续传，可以随时停止和重启一个数据泵任务

### **2.1使用数据泵导出的步骤**

（1）创建目录对象（为输出路径建立一个数据库的directory对象）

```
create directory dump_dir  as  '/datapump/dumps';

create directory log_dir as  ‘/datapump/logs’

删除目录对象
drop directory dump_dir;
```

**注意：还需在电脑上手工创建响应的目录**

（2） 给用户访问权限（需要进行数据库导入和导出的用户）

```
grant read，write on directory dump_dir to  user;

grant read,write on directory dump_dir to scott;
```

**提示：查看数据库中有哪些目录对象 select * from dba_directories;**

（3）选择导出方式，并导出数据库

- 导出整个数据库（加full参数，需要exp_full_datapump角色）

  expdp	user/password 	directory=dump_dir 	dumpfile=dump.dmp	logfile=logging.log	full = y;

- 导出对象模式（加schemas参数，或者同时省略full和schemas参数）

  expdp        user/password	 directory=dump_dir	dumpfile=dump.dmp 	logfile=logging.log	schemas=schemas_name; 

  expdp        user/password	 directory=dump_dir	dumpfile=dump.dmp 	logfile=logging.log; 

- 表(加tables参数)

  expdp 	user/password	directory=dump_dir	dumpfile=dump.dmp 	logfile=logging.log	nologfile=y	content=metadata_only/data_only	tables=table_name1,table_name2......;	

- 表空间(加tablespaces参数，需要exp_full_datapump角色)

  expdp 	user/password	directory=dump_dir	dumpfile=dump.dmp 	logfile=logging.log	tablespaces=tablespace_name1,tablespace_name2......;

- **索引之类的某些对象，在导出时只会导出元数据（内部含有与存储环境有关的具体物理地址），并在导入时重建**
- 完全数据库导出需要用户具有EXP_FULL_DATABASE角色，可以使用system用户实施完全数据库导出
- oracle数据库中有三个较大的角色sysdba , sysoper和dba 。system用户只拥有其中的两项： sysoper和dba ,而sys用户拥有全部三种角色。此外：system用户以sysdba身份登录时就是sys。

### 3.1使用数据泵导入步骤

（1）创建数据导出目录（还需要手动创建该目录，并把dmp文件放到该目录下面）

create or replace directory dump_dir as 'E:\db_oracle\dump';

（2）创建表空间

create tablespace tb_ggj datafile 'E:\db_oracle\tablespace\tb_ggj.dbf' 
size 50m 
autoextend on 
next 50m 
maxsize unlimited 
extent management local;

（3）创建临时表空间

create temporary tablespace temp_tb_ggj tempfile 'E:\db_oracle\tablespace\temp_tb_ggj.dbf' 
size 50m 
autoextend on 
next 50m 
maxsize unlimited 
extent management local;

（4）创建用户

create user rsgl_ggj identified by ggj default tablespace tb_ggj temporary tablespace tb_ggj_temp;

（5）给用户权限

grant read,write on directory dump_dir to rsgl_ggj;
grant dba,resource,unlimited tablespace to rsgl_ggj;

（6）执行Impdp命令

```plsql
impdp rsgl_ggj/rsgl@orcl DIRECTORY=dump_dir  dumpfile=RSGL_GGJ20190416.DMP logfile=rsgl_ggj.log FULL=y 


remap_tablespace=rsgl : rsgl_ggj
```



**善意的提醒：**

- **最好是创建于原来数据库一样的表空间**

## 3、可能用到的命令

**查看管理员目录**

select * from dba_directories;

impdb system/passwd full = y dumpfile=backup:alldb.dmp nologfile=y sqlfile=backup:alldb.sql

**修改用户密码**

alter user RSGL_GGJ identified by rsgl

**查看数据库里面所有用户（前提是你是有dba权限的帐号，如sys,*system）***

select * from dba_users; 

**查看你能管理的所有用户**

select * from all_users;  

**查看当前用户信息** ！

select * from user_users;

**删除账户**

drop user user_name cascade;

**删除表空间**

drop tablespace tb_ggj including contents and datafiles
drop tablespace tb_ggj_temp including contents and datafiles

https://www.cnblogs.com/syforacle/p/5800309.html


