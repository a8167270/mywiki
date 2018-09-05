---
title: "zookeeper安装及配置"
date: 2018-09-05 17:25
---

### 下载

从官网上找到zookeeper安装文件镜像下载

```shell
wget http://mirrors.hust.edu.cn/apache/zookeeper/zookeeper-3.4.13/zookeeper-3.4.13.tar.gz
```

### 解压

```shell
tar –xf zookeeper-3.4.13.tar.gz ./zookeeper
```

### 单机模式

复制conf目录下的`zoo_sample.cfg` ，命名为`zoo.cfg`

修改zoo.cfg的配置文件

```properties
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
dataDir=/datatmp/zookeeper/data
dataLogDir=/datatmp/zookeeper/logs
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
#2888,3888 are election port
server.1=zookeeper:2888:38888
```

### 命令

```shell
# 启动
/bin/zkServer.sh start

# 查看状态
/bin/zkServer.sh status

# 重启
/bin/zkServer.sh restart

# 停止
/bin/zkServer.sh stop
```

## 启动失败原因检查

### 检查MyPID

检查每个节点的`mypid` 文件是否和`zoo.cfg` 匹配

### 检查网络

```shell
telnet 192.168.124.24
```



**No route to host** : 需要关闭服务器防火墙

```shell
sudo iptables -F
```

centos7之后使用的是firewall

```shell
service stop firewall # 关闭防火墙
systemctl disable firewall # 禁止开机启动
```



**Connection refused** : 本地客户端到目标IP地址的路由是正常的，但是该目标端口没有进程在监听，然后服务端拒绝掉了连接。查看zookeeper.out查看具体错误信息：

```verilog
在Log路径下面查看zookeeper.out日志，查看启动记录及报错原因。

​```verilog
2018-01-25 20:37:23,379 [myid:132] - WARN  [WorkerSender[myid=132]:QuorumCnxManager@584] - Cannot open channel to 133 at election address /192.168.233.133:3888
java.net.NoRouteToHostException: No route to host (Host unreachable)
        at java.net.PlainSocketImpl.socketConnect(Native Method)
        at java.net.AbstractPlainSocketImpl.doConnect(AbstractPlainSocketImpl.java:350)
        at java.net.AbstractPlainSocketImpl.connectToAddress(AbstractPlainSocketImpl.java:206)
        at java.net.AbstractPlainSocketImpl.connect(AbstractPlainSocketImpl.java:188)
        at java.net.SocksSocketImpl.connect(SocksSocketImpl.java:392)
        at java.net.Socket.connect(Socket.java:589)
        at org.apache.zookeeper.server.quorum.QuorumCnxManager.connectOne(QuorumCnxManager.java:558)
        at org.apache.zookeeper.server.quorum.QuorumCnxManager.toSend(QuorumCnxManager.java:534)
        at org.apache.zookeeper.server.quorum.FastLeaderElection$Messenger$WorkerSender.process(FastLeaderElection.java:454)
        at org.apache.zookeeper.server.quorum.FastLeaderElection$Messenger$WorkerSender.run(FastLeaderElection.java:435)
        at java.lang.Thread.run(Thread.java:748)
​```
```

**端口占用**

```
netstat -tln | grep 8060 # 检查被占用的端口
lsof -i:8060 # 查找占用这个端口的进程
kill 8060 # kill掉该进程
```

### 客户端连接失败

```verilog
java.net.ConnectException: 拒绝连接
        at sun.nio.ch.SocketChannelImpl.checkConnect(Native Method)
        at sun.nio.ch.SocketChannelImpl.finishConnect(SocketChannelImpl.java:735)
        at org.apache.zookeeper.ClientCnxnSocketNIO.doTransport(ClientCnxnSocketNIO.jav
a:361)
```

如果出现拒绝连接的提示，需要注意到`zoo.cfg`设置的端口号是否是**2181**，因为客户端默认连接的端口是2181，如果是自定义的端口，则在连接的时候，需要制定端口号。

```shell
zkCli.sh -server 192.168.124.130:2183
```

