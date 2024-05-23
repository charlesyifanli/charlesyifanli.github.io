---
title: hive
date: 2024-05-22 21:13:11
tags: hadoop
categories:
- linux config
---

## Preparation

- hadoop3.2.4 has already been installed successfully
- downloaded hive 3.1.2 and mysql jdbc
- pull mysql image and run it

```bash
docker run -p 3306:3306 --name mysql -v ~~/data:~~/data 
-e MYSQL_ROOT_PASSWORD=123123 --privileged=true [images_name]
```



## Config Mysql

### install mysql client

```bash
apt-get update
apt-cache policy mysql-client
apt-get install mysql-client=8.0.?-?ubuntu?

mysql -h ?ip -P 3306 -u myuser -p
```



### operate database

```bash
mysql> create database hive; 
mysql> flush privileges; 
```



## Config Hive

### uncompose hive.tgz file

- mv mysql-connector-java-8.0.28.tar ~~/hive/lib

### remove conflicting jar files **if needed**

- delete ~~/hive/lib/log4j-slf4j-*-2.10.0.jar

### copy and paste higher version

- ~~/hadoop/share/hadoop/common/lib/guava*.jar

- ~~/hive/lib/guava*.jar

### in ~~/hive/conf

```bash
mv hive-default.xml.template hive-default.xml

vim hive-site.xml
```

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
  <property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:mysql://??????????:3306/hive(db_name created)?createDatabaseIfNotExist=true</value>
    <description>JDBC connect string for a JDBC metastore</description>
  </property>
  <property>
    <name>javax.jdo.option.ConnectionDriverName</name>
    <value>com.mysql.jdbc.Driver</value>
    <description>Driver class name for a JDBC metastore</description>
  </property>
  <property>
    <name>javax.jdo.option.ConnectionUserName</name>
    <value>root</value>
    <description>!!!username to use against metastore database</description>
  </property>
  <property>
    <name>javax.jdo.option.ConnectionPassword</name>
    <value>123123</value>
    <description>!!!password to use against metastore database</description>
  </property>
</configuration>
```



## Initialize and start

```bash
schematool -dbType mysql -initSchema -verbose

hive

show databases;
```

