---
title: Terminal Configuration
date: 2023-12-02 21:40:14
tags:
---

## conda

### activate env name automatically

``` bash
$ conda config --set auto_activate_base true
```

More info: [reference](https://www.zhihu.com/question/556021294/answer/2739518322)

### use conda scripts in powershell

``` bash
$ get-ExecutionPolicy
$ set-ExecutionPolicy RemoteSigned
```

More info: [reference](https://zhuanlan.zhihu.com/p/631661770)

## character set configuration

**Display the code page number currently being used by the console:**<br>

```bash
$ chcp
```

**Set the console code page to UTF-8 *temporarily*:**<br>

``` bash
$ chcp 65001
```
