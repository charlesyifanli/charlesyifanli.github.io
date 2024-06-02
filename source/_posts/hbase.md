---
title: hbase
date: 2024-05-17 08:22:24
tags: hadoop
categories:
- linux config
---

## Preparation

- Hadoop has already been installed successfully.
- JDK8 && hadoop3.2.4 && hbase2.4.17 && zookeeper3.7.2



## Zookeeper Config

1. Download and install zookeeper in **/usr/local**(recommended)
2. Run command: **mv zoo_sample.cfg zoo.cfg** in zookeeper/conf
3. Modify zoo.cfg

```reStructuredText
dataDir=/usr/local/zookeeper/data
dataLogDir=/usr/local/zookeeper/log

server.1=master:2888:3888
server.2=slave01:2888:3888
server.3=slave02:2888:3888
```

4. Copy the current folder and paste it to the other hosts

5. In the ~~/zookeeper/data of each computer, create a file named 'myid' and write 1, 2, 3 in each respectively

6. Start each PC respectively

```
/usr/local/zookeeper/bin/zkServer.sh start
```

​       Look through the status

```
/usr/local/zookeeper/bin/zkServer.sh status
```



## HBase Config

### hbase-site.xml

```reStructuredText
  <property>
    <name>hbase.rootdir</name>
    <value>hdfs://master:9000/hbase</value>
  </property>

  <property>
    <name>hbase.cluster.distributed</name>
    <value>true</value> <!--false-->
  </property>

  <property>
    <name>hbase.master.port</name>
    <value>16000</value>
  </property>
  
  <property>
    <name>hbase.master.info.port</name>
    <value>60010</value>
  </property>

  <property>
    <name>hbase.zookeeper.quorum</name>
    <value>master,slave01,slave02</value>
  </property>

  <property>
    <name>hbase.zookeeper.property.clientPort</name>
    <value>2181</value>
  </property>

  <property>
    <name>hbase.zookeeper.property.dataDir</name>
    <value>/usr/local/zookeeper/data</value>
  </property>

  <property>
    <name>hbase.tmp.dir</name>
    <value>./tmp</value>
  </property>

  <property>
    <name>hbase.unsafe.stream.capability.enforce</name>
    <value>false</value>
  </property>
</configuration>
```



### hbase-env.sh

```reStructuredText
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_HOME=/usr/local/hadoop
export HBASE_HOME=/usr/local/hbase
export HBASE_MANAGES_ZK=false
```

and in the last,

uncommit:

```bash
export HBASE_DISABLE_HADOOP_CLASSPATH_LOOKUP="true"
```



### regionservers

```reStructuredText
slave01
slave02
```



**Copy the hbase folder and paste it to the other hosts.**



## Start HBase

- start zookeeper first

Each computer needs to be started.

- start hdfs(hadoop) then

- start hbase

 ```bash
 /usr/local/hbase/bin/start-hbase.sh
 ```



## Deploy

```bash
 hbase thrift -p 9090 start
```

- python connection

```reStructuredText
import happybase

try:
    # Connect to HBase
    connection = happybase.Connection('172.17.0.2', port=9090)

    # Get the names of all tables
    tables = connection.tables()

    # Print the names of all tables
    print("Names of all tables:")
    for table_name in tables:
        print(table_name.decode('utf-8'))

    # Close the connection
    connection.close()

except Exception as e:
    print(f"Error connecting to HBase: {e}")
```





<br>

<br>

## Reference

[Info](https://www.bilibili.com/video/BV1ym4y1w7u6/?spm_id_from=333.337.search-card.all.click&vd_source=f367f43d00246a51bd639e9f1fcda3a9)
