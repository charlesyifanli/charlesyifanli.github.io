---
title: hadoopOperation
date: 2024-05-07 21:29:05
tags: hadoop
categories:
- linux config
---

## Basic Operation

``` reStructuredText
hadoop fs -ls /
```

```reStructuredText
hadoop fs -mkdir -p /user/root
```

```reStructuredText
hadoop fs -test -e /user/root/demo.txt 
if [ $? -eq 0 ]; then
    echo "File exists at path: $file_path"
else
    echo "File does not exist at path: $file_path"
fi
```

```
hadoop fs -put /root/demo.txt /user/root/
hadoop fs -appendToFile /root/demo.txt /user/root/
```

