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



### methods

1. new ~/pip/pip.init
2. update pip.ini

<br>

<br>

## reference

[United Mirrors](https://mirrors.cernet.edu.cn/list)

[Tsinghua](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)

[Info](http://www.manongjc.com/detail/29-ftpasjhctocytqc.html)

