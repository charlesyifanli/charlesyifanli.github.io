---
title: hadoop
date: 2024-04-27 16:33:20
tags: hadoop
categories:
- linux config
---

## Environment Preparation

RockyLinux9.3 && JDK8 && Hadoop3.2.4 



## Basic Operations

### mapping  if needed

```bash
vim /etc/hosts
```

append >> "192.168.2.4 hostname"



### close the firewall if needed

```bash
systemctl stop firewalld
systemctl disable firewalld
```



### handle JDK  and hadoop env variable

in /etc/profile

```reStructuredText
export JAVA_HOME=/root/Downloads/jdk1.8.0_181
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

export HADOOP_HOME=/root/Downloads/hadoop-3.2.4
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
```



## Hadoop Config

###  ?/hadoop-3.2.4/etc/hadoop

#### hadoop-env.sh

```reStructuredText
add >> export JAVA_HOME=/root/Downloads/jdk1.8.0_181
```



#### core-site.xml

```reStructuredText
<configuration>
    <!-- Specify the HDFS nameservice address as charlesyifanli with port 9000 -->
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://charlesyifanli:9000</value>
    </property>
    
    <!-- Specify the directory for storing Hadoop data -->
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/root/Downloads/hadoop-3.2.4/data</value> <!--data folder needs to be created in advance-->
    </property>
</configuration>
```



#### hdfs-site.xml

```reStructuredText
<configuration>
    <!-- The replication factor of HDFS is 1, meaning the data is only saved once -->
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```



#### mapred-site.xml

```reStructuredText
<configuration>
    <!-- Specify that MapReduce runs on YARN -->
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
```



#### yarn-site.xml

```reStructuredText
<configuration>
    <!-- Specify the address of the ResourceManager separately -->
    <property>
       <name>yarn.resourcemanager.hostname</name>
       <value>charlesyifanli</value>
    </property>

    <property>
       <name>yarn.resourcemanager.address</name>
       <value>charlesyifanli:8032</value>
    </property>

    <property>
       <name>yarn.resourcemanager.scheduler.address</name>
       <value>charlesyifanli:8030</value>
    </property>

    <property>
       <name>yarn.resourcemanager.resource-tracker.address</name>
       <value>charlesyifanli:8031</value>
    </property>

    <property>
       <name>yarn.resourcemanager.admin.address</name>
       <value>charlesyifanli:8033</value>
    </property>
    
    <property>
       <name>yarn.resourcemanager.webapp.address</name>
       <value>charlesyifanli:8088</value>
    </property>

    <!-- Specify the MapReduce mode separately -->
    <property>
       <name>yarn.nodemanager.aux-services</name>
       <value>mapreduce_shuffle</value>
    </property>
</configuration>

```



### ?/hadoop-3.2.4/sbin

#### start-dfs.sh && stop-dfs.sh

```reStructuredText
add >> 
HDFS_DATANODE_USER=root
HDFS_DATANODE_SECURE_USER=hdfs
HDFS_NAMENODE_USER=root
HDFS_SECONDARYNAMENODE_USER=root
```



 #### start-yarn.sh && stop-yarn.sh

```reStructuredText
add >>
YARN_RESOURCEMANAGER_USER=root
HADOOP_SECURE_USER=yarn
YARN_NODEMANAGER_USER=root
```



###  ssh config if needed

create public/private keys

```bash
ssh-keygen -t rsa
```



create authorized_keys and change mod

```bash
cd ~/.ssh
touch authorized_keys
chmod 600 authorized_keys
```



add public key into authorized_keys

```bash
cat id_rsa.pub >> authorized_keys
```



## Format and Start Hadoop

### format

```bash
hadoop namenode -format
```



### start && stop hadoop

``` bash
start-all.sh
stop-all.sh
```



### use hadoop

look through the hadoop process

```bash
jps
```

look through port service

```
netstat -tpnl | grep java
```

test:

brower >> http://ip:8088

terminal >> curl http://ip:8088/cluster



<br>

<br>

## reference

[blog](https://zhuanlan.zhihu.com/p/45166521) is partial

[Video](https://www.bilibili.com/video/BV1E4411e7v9/?spm_id_from=333.999.0.0&vd_source=f367f43d00246a51bd639e9f1fcda3a9) is complete

by the way, [Ubunto](https://blog.csdn.net/qq_33980756/article/details/130568379) is here