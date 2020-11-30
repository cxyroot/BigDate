# 1zookeeper是什么

# 2zookeeper的集群配置

| 安装步骤                                                     |
| :----------------------------------------------------------- |
| 1. 解压<br/>2. 把conf文件夹下配置文件改个名字<br/>    cp zoo_sample.cfg zoo.cfg<br/>3. 编辑zoo.cfg,配置datadir<br/>    dataDir=/opt/module/zookeeper-3.4.10/zkData<br/>4. 配置集群机器，每台机器分配一个不同的Serverid<br/>server.2=hadoop102:2888:3888<br/>server.3=hadoop103:2888:3888<br/>server.4=hadoop104:2888:3888<br/>    以上配置2，3，4就是Serverid<br/>5. 在zkData文件夹里新建一个myid文件，内容是本机的Serverid<br/>6. 配置Zookeeper的LogDIR：配置bin/zkEnv.sh文件<br/>    ZOO_LOG_DIR="."改为/opt/module/zookeeper-3.4.10/logs<br/>7. bin/zkServer.sh start |

单机版

集群版

```cfg
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial 
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between 
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just 
# example sakes.
dataDir=/home/soft/zookeeper-3.4.13/zkData
# the port at which the clients will connect
clientPort=2181
# the maximum number of client connections.
# increase this if you need to handle more clients
#maxClientCnxns=60
#
# Be sure to read the maintenance section of the 
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1
server.2=node01:2888:3888
server.3=node02:2888:3888
server.4=node03:2888:3888
```

创建zkData 

创建myid

​	echo 2 > myid

在bin/zkEnv.sh中配置日志路径



# 3zookeeper启动命令

1：启动zookeeper命令

 	bin/zkServer.sh start

2：查看zookeeper状态命令	

​	 bin/zkServer.sh status

# 4zookeeper命令行操作

bin/zkCli.sh  启动zk客户端

ls  /

ls / zookeeper

ls / watch  

create /ttt 123

-s 的用法，如果有重复的，自增，全局自增。

create  -s /ttt1234 abcdef

-e的用法，创建临节点

退出后消失。

create  -e /zxx abcdef



get /ttt

​	数据

get /ttt watch

​	查看节点变化。

caeate /ttt/ppp



status /zookeeper

```
cZxid = 0x0
ctime = Thu Jan 01 08:00:00 CST 1970
mZxid = 0x0
mtime = Thu Jan 01 08:00:00 CST 1970
pZxid = 0x500000005
cversion = 11
dataVersion = 0
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 0
numChildren = 9
```

# 5zookeeper的api操作

## 导入添加pom文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.cxy</groupId>
    <artifactId>ZkDemo001_Api</artifactId>
    <version>1.0-SNAPSHOT</version>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>2.8.2</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.apache.zookeeper/zookeeper -->
        <dependency>
            <groupId>org.apache.zookeeper</groupId>
            <artifactId>zookeeper</artifactId>
            <version>3.4.10</version>
        </dependency>
    </dependencies>

</project>
```



## 准备log日志文件

```properties
log4j.rootLogger=INFO, stdout
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d %p [%c] - %m%n
log4j.appender.logfile=org.apache.log4j.FileAppender
log4j.appender.logfile.File=target/spring.log
log4j.appender.logfile.layout=org.apache.log4j.PatternLayout
log4j.appender.logfile.layout.ConversionPattern=%d %p [%c] - %m%n
```

## java代码

```java
package com.cxy;
import org.apache.zookeeper.*;
import org.apache.zookeeper.data.Stat;
import org.junit.Before;
import org.junit.Test;

import java.util.List;

public class ZooKeeperApi {
    /*public static void main(String[] args) {
        System.out.println("Api");
    }*/
    private static String connectString = "192.168.10.120:2181,192.168.10.101:2181,192.168.10.130:2181";

    private static int sessionTimeout = 2000;

    private ZooKeeper zkClient = null;

    @Before
    public void init() throws Exception {
        zkClient = new ZooKeeper(connectString, sessionTimeout, new
                Watcher() {
                    @Override
                    public void process(WatchedEvent event) {
                        // 收到事件通知后的回调函数（用户的业务逻辑）
                        System.out.println(event.getType() + "--" + event.getPath());
                        // 再次启动监听
                        try {
                            zkClient.getChildren("/", true);
                        } catch (Exception e) {
                            e.printStackTrace();
                        }
                    }
                });
    }

    // 创建子节点
    @Test
    public void create() throws Exception {
        // 参数 1：要创建的节点的路径； 参数 2：节点数据 ； 参数 3：节点权限 ；参数 4：节点的类型
        String nodeCreated = zkClient.create("/abc","jinlian".getBytes(), ZooDefs.Ids.OPEN_ACL_UNSAFE, CreateMode.PERSISTENT);
    }

    // 获取子节点
    @Test
    public void getChildren() throws Exception {
        List<String> children = zkClient.getChildren("/",true);
        for (String child : children) {
            System.out.println(child);
        }
        // 延时阻塞
        Thread.sleep(Long.MAX_VALUE);
    }

    // 判断 znode 是否存在
    @Test
    public void exist() throws Exception {
        Stat stat = zkClient.exists("/hbase", false);
        System.out.println(stat == null ? "not exist" : "exist");
    }
}
```















