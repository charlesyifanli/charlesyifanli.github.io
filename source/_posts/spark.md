---
title: spark
date: 2024-06-04 17:11:25
tags: spark
categories:
- big_data
---

## preparation

- hadoop3.2.4
- spark3.4.3-bin-without-hadoop.tgz

## Procedure

vim ~~/spark/conf/workers

vim ~~/spark/conf/spark-env.sh

add >>

```
export SPARK_DIST_CLASSPATH=$(/usr/local/hadoop-3.2.4/bin/hadoop classpath)
export HADOOP_CONF_DIR=/usr/local/hadoop-3.2.4/etc/hadoop
export SPARK_MASTER_HOST=master
export JAVA_HOME=/usr/local/java8
```



## Test

- cluster >> standalone

```bash
spark-submit --master spark://master:7077 /usr/local/spark/examples/src/main/python/pi.py 2>&1 | grep "Pi is roughly"
```

- cluster >> yarn

```bash
spark-submit --master yarn /usr/local/spark/examples/src/main/python/pi.py 2>&1 | grep "Pi is roughly"
```

