# 01什么是MapReduce

分布式运算程序的编程框架

用户编写的业务逻辑代码和自带默认的

# 02MapReduce的优缺点

优点：MapReduce易于编程（简单），良好的扩展性。

​		   它简单的实现一些接口，就可以完成一个分布式程序。

​			高容错性。适合PB级以上海量数据的离线处理。

缺点：不擅长实时计算，不擅长流式计算，不擅长DAG（有向图）计算

# 03MapReduce核心思想

分为两个阶段

​	Map阶段

​	Reduce阶段

![1568470145740](D:\make\02MapReduce\1568470145740.png)

# 04MapReuce的进程

一个完整的MapReduce程序在分布式运行有3类进程

# 05官网中第一个MapRduce程序

官方文档中的例子，

jar包位置：\hadoop-2.7.2\share\hadoop\mapreduce\hadoop-mapreduce-examples-2.7.2.jar

例子程序：WordCount例子，统计单词。

# 06常用的数据序列号类型

# 07第一个MapReduce程序

pom

```xml

```

3个文件

```java

```

测试流程

```

```

# 08Hadoop的序列化

1. 什么是序列化

2. 为啥要序列化

3. 为啥不用Java序列化

   Java的序列化是一个重量级的序列化框架。

4. hadoop的序列化的特点

   紧凑：高效使用存储空间

   快速：读些数据的的额外开销小

   可扩展：随着通信协议的升级而可升级

   互操作：支持多语言的交互

# 09MpaReduce框架原理

Input ----（InputFormat）--》Mapper----（Shuffle）---》Reducer----（OutputFormat）---》Output

MapTask +ReduceTask=原理

## InputFormat

数据切片与MapTask并行读决定机制



文件====》切片=====》变成KV值====》Shuffle

### MapReduce的详细流程



#### 快速排序

#### 多次归并排序

### Shuffle机制

#### Partition分区

​	Partition告诉数据应该由哪个RdeuceTask来处理。

​	分区号不能跳，要连续。防止浪费资源。

#### 排序















































