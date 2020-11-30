# 1kafka_Api

# 2kafka监控

## KafkaMonitor

1.上传jar包KafkaOffsetMonitor-assembly-0.4.6.jar到集群

2.在/opt/module/下创建kafka-offset-console文件夹

3.将上传的jar包放入刚创建的目录下

4.在/opt/module/kafka-offset-console目录下创建启动脚本start.sh，内容如下：

```shell
#!/bin/bash
java -cp KafkaOffsetMonitor-assembly-0.4.6-SNAPSHOT.jar \
com.quantifind.kafka.offsetapp.OffsetGetterWeb \
--offsetStorage kafka \
--kafkaBrokers hadoop102:9092,hadoop103:9092,hadoop104:9092 \
--kafkaSecurityProtocol PLAINTEXT \
--zk hadoop102:2181,hadoop103:2181,hadoop104:2181 \
--port 8086 \
--refresh 10.seconds \
--retain 2.days \
--dbName offsetapp_kafka &
```

5.在/opt/module/kafka-offset-console目录下创建mobile-logs文件夹

mkdir /opt/module/kafka-offset-console/mobile-logs

6.启动KafkaMonitor

./start.sh

7.登录页面hadoop102:8086端口查看详情

## 

1.上传压缩包kafka-manager-1.3.3.15.zip到集群

2.解压到/opt/module

3.修改配置文件conf/application.conf

kafka-manager.zkhosts="kafka-manager-zookeeper:2181"

修改为：

kafka-manager.zkhosts="hadoop102:2181,hadoop103:2181,hadoop104:2181"

4.启动kafka-manager

bin/kafka-manager

5.登录hadoop102:9000页面查看详细信息