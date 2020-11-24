# 1第一个例子，官方中的圆周率 PI

```
bin/spark-submit \
--class org.apache.spark.examples.SparkPi \
--executor-memory 1G \
--total-executor-cores 2 \
./examples/jars/spark-examples_2.11-2.1.1.jar \
100
```

```
bin/spark-submit \
--class org.apache.spark.examples.SparkPi \
--executor-memory 1G \
--total-executor-cores 2 \
./examples/jars/spark-examples_2.11-2.1.1.jar \
1000000
```



# 2一个监控网址

运行这个命令。如果出来欢迎页面。说明安装没问题。

bin/spark-shell

监控地址

http://192.168.10.120:4040

```
mkdir input
1.txt
2.txt
sc.textFile("input").flatMap(_.split(" ")).map((_,1)).reduceByKey(_+_).collect
```

# 3重要角色

## 		驱动器

## 		执行器

# 4一些模式

## local模式

## standalone模式

## yarn模式（重点）

​		Spark 交个yarn执行

​		yarn的运行流程

## Mesos模式（了解）

# 案例实操

## 

## 

