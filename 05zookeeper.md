# 1zookeeper是什么

# 2zookeeper的集群配置

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

​	





















