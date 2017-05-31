# zookeeper

## 部署zookeeper集群
- `tar xzf zookeeper-3.4.10.tar.gz`
- `mkdir -p zookeeper-3.4.10/{logs,zk-data}`
- `cp zookeeper-3.4.10/conf/zoo_sample.cfg zookeeper-3.4.10/conf/zoo.cfg`
- `vi zookeeper-3.4.10/conf/zoo.cfg`
```bash
    tickTime=2000
    initLimit=10
    syncLimit=5
    dataDir=/wapp/uniiof/tstusers/uiptstzkp01/zookeeper-3.4.10/zk-data
    clientPort=22181
    server.1=WegTstWeb01:29999:39999
    server.2=WegTst01:29999:39999
    server.3=WegTst02:29999:39999
```
- `vi zookeeper-3.4.10/bin/zkEnv.sh`
```bash
    export JAVA_HOME=/wapp/freeware/jdk1.7.0_51
    export PATH=.:$JAVA_HOME/bin:$PATH
    export ZOOCFGDIR=~/zookeeper-3.4.10/conf
    export ZOO_LOG_DIR=~/zookeeper-3.4.10/logs
    export ZOOBINDIR=~/zookeeper-3.4.10/bin
    export ZOOKEEPER_PREFIX=~/zookeeper-3.4.10
    export CLASSPATH=~/zookeeper-3.4.10/lib:${CLASSPATH}
```
- `vi zookeeper-3.4.10/zk-data/myid`
> WegTstWeb01 : 1
```bash
    1
```
> WegTst01 : 2
```bash
    2
```
> WegTst02 : 3
```bash
    3
```

## 启/停zookeeper集群
`bash zookeeper-3.4.10/bin/zkServer.sh start`

`bash zookeeper-3.4.10/bin/zkServer.sh stop`