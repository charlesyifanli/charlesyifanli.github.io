---
title: hbase
date: 2024-05-17 08:22:24
tags: hadoop
categories:
- linux config
---

## Preparation

- Hadoop has already been installed successfully.
- JDK8 && hadoop3.2.4 && hbase2.3.4 && zookeeper3.5.9



## Zookeeper Config

1. Download and install zookeeper in **/usr/local**(recommended)
2. Run command: **mv zoo_sample.cfg zoo.cfg** in zookeeper/conf
3. Modify zoo.cfg

```reStructuredText
dataDir=/usr/local/zookeeper/data # (create first)
dataLogDir=/usr/local/zookeeper/log # (create first)

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

