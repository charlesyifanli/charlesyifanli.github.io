---
title: Conda and Pip
date: 2024-02-08 19:25:44
tags: mirror
categories:
- mirror config
---

## conda config

### view mirror sources

```bash
$ conda config --show-sources
```



### display config file 

```bash
$ conda config --set show_channel_urls yes
```

update ~/.condarc



### example

```
channels:
  - defaults
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

ssl_verify: true
show_channel_urls: true
auto_activate_base: false
```





### create and delete envs

```bash
$ conda create -n <env_name> [python=3.10]
$ conda remove -n <environment_name> --all
```



### clear cache index

```bash
$ conda clean -i
```



<br>

<br>



## pip

### view mirror sources

```bash
$ pip config list
```

[pip command line](https://pip.pypa.io/en/stable/cli/)



### methods

####  windows

1. new ~/pip/pip.init
2. update pip.ini

#### linux

1. new ~/.config/pip/pip.conf
2. update pip.conf



### example

```
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```

```
[global]
index-url = https://mirror.nju.edu.cn/pypi/web/simple
[install]
trusted-host = https://mirror.nju.edu.cn/pypi/web
```





<br>

<br>

## reference

[United Mirrors](https://mirrors.cernet.edu.cn/list)

[Tsinghua](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)

[Info](http://www.manongjc.com/detail/29-ftpasjhctocytqc.html)

[Linux](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

