---
title: docker
date: 2024-04-26 18:14:00
tags: 
- docker
categories:
- docker
---

## Basic Operation

### create &&  query && delete image

```bash
docker build -t repo_name:tag .
```

```bash
docker images
```

```bash
docker rmi repo_name:tag/id
```



### run && query && delete container

```bash
docker run [-it/-d] [-p host_port:container_port] [-v /host/data:/container/data] 
--name container_name --hostname hostname repo_name:tag
```

- -it: interact with current console
- -d: detach
- -p: set port
- -v: set volume

```bash
docker ps [-a]
```

```bash
docker rm container_name/id
```



### start && stop container

```bash
docker start/stop container_name
```

```bash
docker exec -it container_name  bash
docker attach container_name
```

- interact with current console



## Docker and Github Package

### preparation

 github >>  settings >> developer settings >> get the token with **privilege** "write packages"

### operations

docker login

```bash
docker login ghcr.io -u [github name]  -p [token]
```



image format

```reStructuredText
ghcr.io/[github name]/repo_name/image_name:tag  # [full_image_name == repo_name/image_name]
```



push && pull

```bash
docker push ghcr.io/[github name]/repo_name/image_name:v1.2  # [full_image_name == repo_name/image_name]

docker pull ghcr.io/[github name]/repo_name/image_name:v1.2  # [full_image_name == repo_name/image_name]
```



exit

```
docker logout
```



## Docker Network

- list docker network

```bash
docker network list
```

- inspect

```bash
docker network inspect [name] | less
```

-  view the IP address information on the network device `veth_name`, output it in JSON format, and use `jq` to format and process the JSON data.

```bash
ip -json address show dev [veth_name] | jq
```





##  reference

[Info](https://blog.csdn.net/github_38294679/article/details/135754374?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171412000316800225517633%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=171412000316800225517633&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-135754374-null-null.142^v100^pc_search_result_base2&utm_term=docker%E5%A6%82%E4%BD%95%E5%B0%86%E9%95%9C%E5%83%8F%E5%AD%98%E5%82%A8%E5%88%B0github&spm=1018.2226.3001.4187)

[Network](https://www.bilibili.com/video/BV1Aj411r71b/?spm_id_from=333.999.0.0&vd_source=f367f43d00246a51bd639e9f1fcda3a9)
