---
title: hadoop
date: 2024-04-27 16:33:20
tags: hadoop
categories:
- linux
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

###  

