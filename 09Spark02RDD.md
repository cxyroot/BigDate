

# 1java IO

​                 输入和输出

 				字节流（rar，zip，dat，图片）和字符流（txt）

```java
		//java io 的设计模式：装饰者设计模式
        //InputStream in= FileInputStream("");
        //InputStream buffer =new BufferedInputStream(new FileInputStream(""));
```



## 2RDD

RDD体现了装饰者设计模式。将数据处理的逻辑进行封装。控制抽象。

## 什么是RDD

弹性式分布式数据集.是Spark中最基本的数据（计算）抽象。代码中是一个抽象类。

它代表一个**不可变**，**可分区**、里面元素**可并行计算**的的集合。

## RDD的属性

1. 一组分区 ，即数据集的基本组成单位
2. 一个计算每一个分区的函数
3. RDD之间的依赖关系
4. 一个Partitioner，即RDD的分片函数
5. 一个列表，存储每一个Partition的优先位置。

（移动数据不如移动计算:优先位置的问题。） 

RDD的特点

​	分区，并行计算

​	只读

​	依赖（血缘关系）

​	缓存（缓存操作，防止数据丢失。）



# 2算子（分步简化问题）

什么是算子。认知心理学

**解决的问题其实就是将问题的初始状态，通过一系列的操作对问题的状态进行转换，然后达到完成的状态**

算子===》操作



Spark 的算子 的功能不同。Spark中的所有RDD方法

- 转换算子 
- 行动算子

# 3RDD的创建

​		从集合中创建  内存集合创建

```scala
	val config:SparkConf = new SparkConf().setMaster("local[*]").setAppName("WordCount")
    val sc = new SparkContext(config)
    val listRDD:RDD[Int] = sc.makeRDD(List(1,2,3,4));
    listRDD.collect().foreach(print)
```

```scala
	val config:SparkConf = new SparkConf().setMaster("local[*]").setAppName("WordCount")
    val sc = new SparkContext(config)
    val arrayRDD:RDD[Int] = sc.parallelize(Array(1,2,3,4));
    arrayRDD.collect().foreach(print)
```

​	

​		从外部存储创建RDD

​		

```scala
 val config:SparkConf = new SparkConf().setMaster("local[*]").setAppName("WordCount");

 val sc = new SparkContext(config)

 println(sc);
 //文件中读取的都是字符串类型的
 var lines :RDD[String] = sc.textFile("in/word.txt")
```

​		从其他RDD创建



RDD的自定义分区

```scala
val config:SparkConf = new SparkConf().setMaster("local[*]").setAppName("WordCount")
val sc = new SparkContext(config)
//设置分区 makeRDD中方法有源码。local按照当前的cpu来分区
//
val listRDD:RDD[Int] = sc.makeRDD(List(1,2,3,4),2);
listRDD.saveAsObjectFile("out")
```

```scala
val config:SparkConf = new SparkConf().setMaster("local[*]").setAppName("WordCount")
val sc = new SparkContext(config)
//设置分区
var lines :RDD[String] = sc.textFile("in/word.txt",2)
lines.saveAsObjectFile("out")
```









































