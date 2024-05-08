---
title: hadoop
date: 2024-04-27 16:33:20
tags: hadoop
categories:
- linux config
---

## Hadoop Cluster

RockyLinux9.3 && Docker && JDK8 && Hadoop3.2.4 (jdk21 is NOT compatible with hadoop3.4.0)



## Basic Operations If Needed

### mapping 

```bash
vim /etc/hosts
```

append >> "192.168.2.4 hostname"



### close the firewall

```bash
systemctl stop firewalld
systemctl disable firewalld
```



### handle JDK  and hadoop env variable

in /etc/profile or ~/.bashrc:

```reStructuredText
export JAVA_HOME=/root/Downloads/jdk1.8.0_181
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

export HADOOP_HOME=/root/Downloads/hadoop-3.2.4
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
```



## Docker Image with hadoop installed

###   /path/hadoop-3.2.4/etc/hadoop

#### hadoop-env.sh

```bash
export JAVA_HOME=/root/Downloads/jdk1.8.0_181
```



#### core-site.xml

```reStructuredText
<configuration>
      <property>
          <name>hadoop.tmp.dir</name>
          <value>file:/usr/local/hadoop/tmp</value>
          <description>Abase for other temporary directories.</description>
      </property>
      <property>
          <name>fs.defaultFS</name>
          <value>hdfs://master:9000</value>
      </property>
</configuration>
```



#### hdfs-site.xml

```reStructuredText
<configuration>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/usr/local/hadoop/namenode_dir</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/usr/local/hadoop/datanode_dir</value>
    </property>
    <property>
        <name>dfs.replication</name>
        <value>2</value>
    </property>
</configuration>
```



#### mapred-site.xml

```reStructuredText
  <configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
  </configuration>
```



#### yarn-site.xml

```reStructuredText
 <configuration>
  <!-- Site specific YARN configuration properties -->
      <property>
          <name>yarn.nodemanager.aux-services</name>
          <value>mapreduce_shuffle</value>
      </property>
      <property>
          <name>yarn.resourcemanager.hostname</name>
          <value>master</value>
      </property>
  </configuration>
```



### /path/hadoop-3.2.4/sbin if  root needed 

#### start-all.sh && stop-all.sh

```bash
export HDFS_NAMENODE_USER=root
export HDFS_DATANODE_USER=root
export HDFS_SECONDARYNAMENODE_USER=root
export YARN_RESOURCEMANAGER_USER=root
export YARN_NODEMANAGER_USER=root
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



### create image

```bash
docker commit [container_id/name] [image_name]
```



## Config master and slaves

### create containers:

```bash
docker run -it [-v ~/hadoopMapping/hosts:/etc/hosts] -h master --name master ubuntu/hadoopinstalled

docker run -it [-v ~/hadoopMapping/hosts:/etc/hosts] -h slave01 --name slave01 ubuntu/hadoopinstalled

docker run -it [-v ~/hadoopMapping/hosts:/etc/hosts] -h slave02 --name slave02 ubuntu/hadoopinstalled
```

- If needed(hostname <==> ip address), [-v path/hosts:/etc/hosts] **or** create new docker network.



### add slave computer

vim /path/hadoop/etc/hadoop/workers,

replace localhost with the hostnames of two slaves.



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

## Reference

[blog](https://dblab.xmu.edu.cn/blog/1233/)
