# 1kafka简介



削峰填谷



## kafka的主要架构

1 ）Producer  ：消息生产者，就是向 kafka broker 发消息的客户端；
2 ）Consumer  ：消息消费者，向 kafka broker 取消息的客户端；
3 ）Consumer Group  （CG） ）： ：消费者组，由多个 consumer 组成。 消费者组内每个消费者负
责消费不同分区的数据，一个分区只能由一个消费者消费；消费者组之间互不影响。所有
的消费者都属于某个消费者组，即 消费者组是逻辑上的一个订阅者。
4 ）Broker  ：一台 kafka 服务器就是一个 broker。一个集群由多个 broker 组成。一个 broker
可以容纳多个 topic。
5 ）Topic ： ：可以理解为一个队列，个
生产者和消费者面向的都是一个 topic；
6 ）Partition ：为了实现扩展性，一个非常大的 topic 可以分布到多个 broker（即服务器）上，
个 一个 topic  可以分为多个 partition，每个 partition 是一个有序的队列；
7 ）Replica ：副本，为保证集群中的某个节点发生故障时，该节点上的 partition 数据不丢失，
且 kafka 仍然能够继续工作，kafka 提供了副本机制，一个 topic 的每个分区都有若干个副本，
一个 leader 和若干个 follower。
8 ）leader： ：每个分区多个副本的“主”，生产者发送数据的对象，以及消费者消费数据的
对象都是 leader。
9 ）follower ：每个分区多个副本中的“从”，实时从 leader 中同步数据，保持和 leader 数据
的同步。leader 发生故障时，某个 follower 会成为新的 follower。

# 2配置kafka集群

## 1：下载安装包

## 2：解压安装包到/home/soft/

## 3：修改名称 

## 4：创建logs文件

## 	mkdir logs

## 5：进入config，修改 vim server.properties 

```ini
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# see kafka.server.KafkaConfig for additional details and defaults

############################# Server Basics #############################

# The id of the broker. This must be set to a unique integer for each broker.
# 不同机器上的broker.id 不相同。
broker.id=0

# Switch to enable topic deletion or not, default value is false
# 需要放开内容
delete.topic.enable=true

############################# Socket Server Settings #############################

# The address the socket server listens on. It will get the value returned from 
# java.net.InetAddress.getCanonicalHostName() if not configured.
#   FORMAT:
#     listeners = listener_name://host_name:port
#   EXAMPLE:
#     listeners = PLAINTEXT://your.host.name:9092
#listeners=PLAINTEXT://:9092

# Hostname and port the broker will advertise to producers and consumers. If not set, 
# it uses the value for "listeners" if configured.  Otherwise, it will use the value
# returned from java.net.InetAddress.getCanonicalHostName().
#advertised.listeners=PLAINTEXT://your.host.name:9092

# Maps listener names to security protocols, the default is for them to be the same. See the config documentation for more details
#listener.security.protocol.map=PLAINTEXT:PLAINTEXT,SSL:SSL,SASL_PLAINTEXT:SASL_PLAINTEXT,SASL_SSL:SASL_SSL

# The number of threads that the server uses for receiving requests from the network and sending responses to the network
num.network.threads=3

# The number of threads that the server uses for processing requests, which may include disk I/O
num.io.threads=8

# The send buffer (SO_SNDBUF) used by the socket server
socket.send.buffer.bytes=102400

# The receive buffer (SO_RCVBUF) used by the socket server
socket.receive.buffer.byt es=102400

# The maximum size of a request that the socket server will accept (protection against OOM)
socket.request.max.bytes=104857600


############################# Log Basics #############################

# A comma seperated list of directories under which to store log files
# 日志路径配置
log.dirs=/home/soft/kafka/logs

# The default number of log partitions per topic. More partitions allow greater
# parallelism for consumption, but this will also result in more files across
# the brokers.
num.partitions=1

# The number of threads per data directory to be used for log recovery at startup and flushing at shutdown.
# This value is recommended to be increased for installations with data dirs located in RAID array.
num.recovery.threads.per.data.dir=1

############################# Internal Topic Settings  #############################
# The replication factor for the group metadata internal topics "__consumer_offsets" and "__transaction_state"
# For anything other than development testing, a value greater than 1 is recommended for to ensure availability such as 3.
offsets.topic.replication.factor=1
transaction.state.log.replication.factor=1
transaction.state.log.min.isr=1

############################# Log Flush Policy #############################

# Messages are immediately written to the filesystem but by default we only fsync() to sync
# the OS cache lazily. The following configurations control the flush of data to disk.
# There are a few important trade-offs here:
#    1. Durability: Unflushed data may be lost if you are not using replication.
#    2. Latency: Very large flush intervals may lead to latency spikes when the flush does occur as there will be a lot of data to flush.
#    3. Throughput: The flush is generally the most expensive operation, and a small flush interval may lead to exceessive seeks.
# The settings below allow one to configure the flush policy to flush data after a period of time or
# every N messages (or both). This can be done globally and overridden on a per-topic basis.

# The number of messages to accept before forcing a flush of data to disk
#log.flush.interval.messages=10000

# The maximum amount of time a message can sit in a log before we force a flush
#log.flush.interval.ms=1000

############################# Log Retention Policy #############################

# The following configurations control the disposal of log segments. The policy can
# be set to delete segments after a period of time, or after a given size has accumulated.
# A segment will be deleted whenever *either* of these criteria are met. Deletion always happens
# from the end of the log.

# The minimum age of a log file to be eligible for deletion due to age
log.retention.hours=168

# A size-based retention policy for logs. Segments are pruned from the log as long as the remaining
# segments don't drop below log.retention.bytes. Functions independently of log.retention.hours.
#log.retention.bytes=1073741824

# The maximum size of a log segment file. When this size is reached a new log segment will be created.
log.segment.bytes=1073741824

# The interval at which log segments are checked to see if they can be deleted according
# to the retention policies
log.retention.check.interval.ms=300000

############################# Zookeeper #############################

# Zookeeper connection string (see zookeeper docs for details).
# This is a comma separated host:port pairs, each corresponding to a zk
# server. e.g. "127.0.0.1:3000,127.0.0.1:3001,127.0.0.1:3002".
# You can also append an optional chroot string to the urls to specify the
# root directory for all kafka znodes.
# 集群配置
zookeeper.connect=node01:2181,node02:2181,node03:2181

# Timeout in ms for connecting to zookeeper
zookeeper.connection.timeout.ms=6000


############################# Group Coordinator Settings #############################

# The following configuration specifies the time, in milliseconds, that the GroupCoordinator will delay the initial consumer rebalance.
# The rebalance will be further delayed by the value of group.initial.rebalance.delay.ms as new members join the group, up to a maximum of max.poll.interval.ms.
# The default value for this is 3 seconds.
# We override this to 0 here as it makes for a better out-of-the-box experience for development and testing.
# However, in production environments the default value of 3 seconds is more suitable as this will help to avoid unnecessary, and potentially expensive, rebalances during application startup.
group.initial.rebalance.delay.ms=0

```

## 6：配置集群

已经配置完成主要是修改server.properties

## 7：逐个启动集群（3台机器）

先启动zk

1：启动zookeeper命令

 	bin/zkServer.sh start

2：查看zookeeper状态命令	

​	 bin/zkServer.sh status

### 默认启动：

​				bin/zkServer.sh start

### 启动命令

​				bin/kafka-server-start.sh  -daemon  config/server.properties

## 8群起脚本

```shell
#! /bin/bash

case $1 in
"start"){
        for i in hadoop102 hadoop103 hadoop104
        do
                echo " --------启动 $i Kafka-------"
                # 用于KafkaManager监控
                ssh $i "export JMX_PORT=9988 && /home/soft/kafka/bin/kafka-server-start.sh -daemon /home/soft/kafka/config/server.properties "
        done
};;
"stop"){
        for i in hadoop102 hadoop103 hadoop104
        do
                echo " --------停止 $i Kafka-------"
                ssh $i "/home/soft/kafka/bin/kafka-server-stop.sh stop"
        done
};;
esac
```



### 后台启动：



# 3kafka命令行操作

## 1:查询分区

bin/kafka-topics.sh  

可以查看命令简述

bin/kafka-topics.sh --zookeeper node01:2181 --list

为什么要指定zookeeper ？

## 2:创建分区topics 

first 为名字

3为分区副本数据

2为定义的分区数

bin/kafka-topics.sh --zookeeper node01:2181 --create --topic  first  --partitions  3 --replication-factor 2



bin/kafka-topics.sh --zookeeper node01:2181 --create --replication-factor 3 --partitions 1 --topic   



修改分区数

topics的分区 数量只能增加

bin/kafka-topics.sh --zookeeper node01:2181 --alter --partitions  5 --topic first

## 3：查看topic的详情

bin/kafka-topics.sh --zookeeper node01:2181 --describe --topic first

![image-20201124210355628](D:\Note\06kafka\image-20201124210355628.png)

## 4：生产者生产消息

​	flume 到kafka 

​    producer 生产者

​	9092kafka固定端口号

​	bin/kafka-console-producer.sh  --topic first --broker-list  node01:9092

## 5：消费者消费消息

​    consumer  消费者  

​	bin/kafka-console-consumer.sh --topic first --zookeeper node01:2181 

​	bin/kafka-console-consumer.sh --topic first --bootstrap-server node01:9092

## 6：消费历史消息

   --from-beginning --topic first

# 4Kafka工作流程

Kafka 中消息是以 topic 进行分类的，生产者生产消息，消费者消费消息，都是面向 topic的。topic 是逻辑上的概念，而 partition 是物理上的概念，每个 partition 对应于一个 log 文件，该 log 文件中存储的就是 producer 生产的数据。Producer 生产的数据会被不断追加到该 log文件末端，且每条数据都有自己的 offset。消费者组中的每个消费者，都会实时记录自己消
费到了哪个 offset，以便出错恢复时，从上次的位置继续消费。

# 5kafka文件存储机制

生产者将数据发给topic 消费者从topic消费数据



一个topic多个 partition    一个partition 多个segment。每个 segment对应两个文件——“.index”文件和“.log”文件。



## 6kafka生产者

​			分区策略	1为啥要分区2分区的原则

为什么半数以上同意才能选出leader

​	防止脑裂

参与投票的follower至少有多少

​	半数以上

如何保证参与投票的半数以上的follower里面至少有一个同步完成

​	半数以上的follower同步完成

数据可靠性保证

Exactly Once语义



​			

## 7kafka消费者

消费方式

​	以下游的的速率去消费数据，缺点是容易空循环   使用timeout时间去优化空循环

分区分配策略，两种分区分配策略。

​	

ofeset的维护

# 8kafka高效读写数据

顺序写磁盘   一直向文件的末端增加数据  

零复制技术（零拷贝的概念）

​	   不经过用户层   直接在内核层交互

# 9zk在kafka中的作用



