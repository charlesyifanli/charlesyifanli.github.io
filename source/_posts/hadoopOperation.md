---
title: hadoopOperation
date: 2024-05-07 21:29:05
tags: hadoop
categories:
- big_data
---

## Basic Operation

### read folder and file information

``` bash
hdfs dfs -ls [-R] [-h] /
```

- recursive
- human-readable



### create/remove  file/folder

```bash
hdfs dfs -mkdir -p /user/root

hdfs dfs -touchz /path/to/hdfs/emptyfile

hdfs dfs -rm [-rf] /path/to/hdfs/directory_or_file
```



### judge existence and look through

```bash
hdfs dfs  -test -e /user/root/demo.txt
echo $?

hdfs dfs -cat /user/root/demo.txt
```



### upload && download && append file

```bash
hdfs dfs -put [-f] demo.txt /user/root
hdfs dfs -get demo.txt /root/

hdfs dfs -appendToFile /root/demo.txt /user/root/demo.txt
hdfs dfs -copyFromLocal [-f] /root/demo.txt /user/root/demo.txt
```



### move or rename file

```bash
hdfs dfs -mv test.txt dir/test.txt
```

