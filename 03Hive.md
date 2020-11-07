# 01:Hive基本概念

将HQL转换为MapReduce程序：

​	Hive的数据存储在Hdfs上

​	hive分析数据传递称的实现是MapReduce

​	执行程序运行在YARN上



Hive的架构



Hive常用于数据分析，对实实时性要求不高



Hive和数据库比较

​		查询语言

​	    数据存储位置

​		数据更新

​	 	索引

​		执行

​		执行延迟

# 02Hive安装准备

版本，新特性

安装准备

​	

​	start-dfs.sh  启动dataNode和nameNode

​	start-yarn.sh 开启ResourceManager





安装

​	bin/hive  启动 hive命令

启动hive 

​	bin/hive

查询数据库

​	show database；

打开默认数据库

​	use default

显示default中的表

​	show tables

创建一张表

​	 create  table student(id int,name string)  ;

​	 create  table student(id int,name string)  row format delimited fields terminated by '\t';

查看表的结构

​	desc student;

插入数据

​	insert  into student values(001,'caoxiaoyang');

​	插入的时候，使用hadoop的hdfs

查询表中的数据

​	select  *from studnet;

退出hive

​	quit;

# 03将本地文件导入到hive中

创建表

```sql
create table student(id int, name string) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t';
```

```sql
load data local inpath '/home/soft/datas/student.txt' into table student;
```



# 04数据库的基本使用

mysql  -uroot -p123456

mysql表中主机配置

​	use mysql;

​	select host,user,password from user;

+------+------+-------------------------------------------+
| host | user | password                                  |
+------+------+-------------------------------------------+
| %    | root | *6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9 |
+------+------+-------------------------------------------+
1 row in set (0.00 sec)

## 配置hive元数据到mysql

​		service mysql status    查看本机 mysql启动状态.



bin/hive -e  'select *from student;'  不启动hive,直接查询结果

bin/hive -f ./hsql.sql   使用外部的sql文件查询结果.



hive中查看hdfs文件系统中的内容

dfs  -lsr /user;

# 05一些基本命令操作

## 查看本地系统中的内容。

!ls  /opt;

## 查看hive 历史运行的命令

​		[root@node01 ~]# cat .hivehistory 

## 显示当前数据库，以及查询表的头信息配置

```xml
<!-- 显示当前数据库，以及查询表的头信息配置 -->
<property>
	<name>hive.cli.print.header</name>
	<value>true</value>
</property>

<property>
	<name>hive.cli.print.current.db</name>
	<value>true</value>
</property>
```

## 查看hive所有的配置信息

set;    -- 查看hive所有的配置信息

## 修改hive中的默认日志配置

​	mv  hive-log4j.properties.temp  hive-log4j.properties

​    vi  hive-log4j.properties

```properties
hive.log.threshold=ALL 
hive.root.logger=INFO,DRFA
hive.log.dir=/home/soft/hive/logs
hive.log.file=hive.log
```

## 配置的优先级

文件配置





# 06数据类型

基本数据类型

集合数据类型





# 07DDL数据定义

## 创建数据库

​	创建数据库

​		create database db_hive;

   创建数据库，如果存在则不创建

​    create database if not exists db_hive;

​	创建数据库，指定创建位置

​    create database if not exists db_hive2

​			location ' /db_hive2.db'  ---/为hadoop下的目录，查看地址为[http://192.168.10.120:50070](http://192.168.10.120:50070/)

## 修改数据库

​	  只能修改配置信息，不能修改数据库名和数据库所在位置。

​		desc database db_hive

​	  在mysql中查看修改结果

​     	desc database extended db_hive

查询数据库

​	show databases;

 	show databases like 'db*'

​     显示数据库信息。

​		desc db_hive;

​		use db_hive;

​		show tables;

## 删除数据库

​	删除空数据库

​      drop database db_hive;

​	  drop database  if exists db_hive;

​	  show databases;

​	删除有数据的数据库

​		 drop database if exists  db_hive cascade;

## 创建表 

### 内部表管理表	

​	创建表语句

```sql
create table if not exists student2(
id int, name string
)
row format delimited fields terminated by '\t'
stored as textfile
location '/user/hive/warehouse/student';
```

​	迁移数据，相当于生成备份表

```sql
create table if not exists student3
as select id, name from student;
```

​	只创建表不迁移数据。

```sql
create table if not exists student4 like student;
```

​	删除表及数据

```sql
 drop table student;
```

### 外部表

外部表：项目组可以同时操作一个表，主要进行查询。	

创建外部表。 -- external

```sql
create external table if not exists dept(
deptno int,
dname string,
loc int
)
row format delimited fields terminated by '\t';

```

### 分区表

创建分区表。--partitioned by (month string)

```sql
create table dept_partition(
               deptno int, dname string, loc string
 ) partitioned by (month string)
 row format delimited fields terminated by '\t';
```

加载数据到分区表



# 08DML数据库定义

## 数据导入

​		加载本地文件到hive

```sql
load data local input /opt/home/soft/student.txt into table student
```

​	   加载hdfs文件到hive    

```
dfs -put /opt/student.txt / --上传数据到hdfs中
load data input '/student.txt' into table student;
```

  加载数据覆盖表中已有数据 --overwrite

```sql
load data local input /opt/home/soft/student.txt overwrite into table student
```

创建分区表

```sql
create table student(
     deptno int, dname string
 ) partitioned by (month string)
 row format delimited fields terminated by '\t';
```

```sql
insert into table student partition(month ='2019') values(100,'张三'，);
```

```sql
insert overwrite table student partition(month='201708') select id,name from student where month='201709';
```

```sql
from student 
insert overwrite table student partition(month='201708') 
select id,name from student where month='201709'
insert overwrite table student partition(month='201708') 
select id,name from student where month='201709'
```

location 加载数据

```sql
create table student2
     deptno int, dname string
 ) row format delimited fields terminated by '\t'
 location '/user/hive/warehouse/student2';
```

上传数据到hdfs上。

```
dfs -put /opt/student.txt   /user/hive/warehouse/student2 ;
```



## 数据导出



insert 导出数据。



## 清除表中的数据






Hive是基于Hadoop的一个数据仓库工具，可以将结构化的数据文件映射为一张数据库表，并提供简单的sql查询功能，可以将sql语句转换为MapReduce任务进行运行。HBase是Hadoop的数据库，一个分布式、可扩展、大数据的存储。单个的从字面意思上或许很难看出二者的区别，别急，下面我们就对二者做个详细的介绍。

两者的特点


hive和hbase的区别。
      Hive帮助熟悉SQL的人运行MapReduce任务。因为它是JDBC兼容的，同时，它也能够和现存的SQL工具整合在一起。运行Hive查询会花费很长时间，因为它会默认遍历表中所有的数据。虽然有这样的缺点，一次遍历的数据量可以通过Hive的分区机制来控制。分区允许在数据集上运行过滤查询，这些数据集存储在不同的文件夹内，查询的时候只遍历指定文件夹(分区)中的数据。这种机制可以用来，例如，只处理在某一个时间范围内的文件，只要这些文件名中包括了时间格式。

      HBase通过存储key/value来工作。它支持四种主要的操作：增加或者更新行，查看一个范围内的cell，获取指定的行，删除指定的行、列或者是列的版本。版本信息用来获取历史数据(每一行的历史数据可以被删除，然后通过Hbase compactions就可以释放出空间)。虽然HBase包括表格，但是schema仅仅被表格和列簇所要求，列不需要schema。Hbase的表格包括增加/计数功能。

限制

Hive目前不支持更新操作。另外，由于hive在hadoop上运行批量操作，它需要花费很长的时间，通常是几分钟到几个小时才可以获取到查询的结果。Hive必须提供预先定义好的schema将文件和目录映射到列，并且Hive与ACID不兼容。

HBase查询是通过特定的语言来编写的，这种语言需要重新学习。类SQL的功能可以通过Apache Phonenix实现，但这是以必须提供schema为代价的。另外，Hbase也并不是兼容所有的ACID特性，虽然它支持某些特性。最后但不是最重要的–为了运行Hbase，Zookeeper是必须的，zookeeper是一个用来进行分布式协调的服务，这些服务包括配置服务，维护元信息和命名空间服务。

应用场景

Hive适合用来对一段时间内的数据进行分析查询，例如，用来计算趋势或者网站的日志。Hive不应该用来进行实时的查询。因为它需要很长时间才可以返回结果。

Hbase非常适合用来进行大数据的实时查询。Facebook用Hbase进行消息和实时的分析。它也可以用来统计Facebook的连接数。

总结

Hive和Hbase是两种基于Hadoop的不同技术–Hive是一种类SQL的引擎，并且运行MapReduce任务，Hbase是一种在Hadoop之上的NoSQL 的Key/vale数据库。当然，这两种工具是可以同时使用的。就像用


