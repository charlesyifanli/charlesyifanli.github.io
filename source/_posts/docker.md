---
title: docker
date: 2024-04-26 18:14:00
tags: 
- docker
categories:
- docker
---

## Common Command

1. **Pull an image**:
    - `docker pull [image]`: Pulls a specified image from Docker Hub or other image repositories.
  
2. **Create and run a container**:
    - `docker run [options] [image]`: Creates and runs a new container using the specified image. Common options include:
        - `-d`: Runs the container in the background.
        - `-p [host_port]:[container_port]`: Maps a host port to a container port.
        - `-v [host_path]:[container_path]`: Mounts a host folder to a container folder.
        - `--name [name]`: Assigns a name to the container.
    - Example: `docker run -d -p 8080:80 --name my-container nginx`

3. **List containers**:
    - `docker ps`: Lists running containers.
    - `docker ps -a`: Lists all containers, including stopped ones.

4. **Stop a container**:
    - `docker stop [container]`: Stops the specified container.

5. **Remove a container**:
    - `docker rm [container]`: Removes the specified container.

6. **List images**:
    - `docker images`: Lists locally stored images.

7. **Remove an image**:
    - `docker rmi [image]`: Removes the specified image.

8. **Execute a command**:
    - `docker exec [options] [container] [command]`: Executes a command in the specified container. Common options include:
        - `-d`: Executes the command in the background.
        - `-it`: Runs interactively.
    - Example: `docker exec -it my-container /bin/bash`

9. **View container logs**:
    - `docker logs [options] [container]`: Views logs for the specified container. Common options include:
        - `-f`: Follow mode for real-time logs.

10. **Build an image**:
    - `docker build [options] [path]`: Builds an image using a Dockerfile. Common options include:
        - `-t [name]`: Tags the built image.
    - Example: `docker build -t my-image .`

11. **Inspect container details**:
    - `docker inspect [container]`: Inspects details of the specified container.

12. **Log in to Docker Hub**:
    - `docker login`: Logs in to Docker Hub account.



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



### reference

[Info](https://blog.csdn.net/github_38294679/article/details/135754374?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171412000316800225517633%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=171412000316800225517633&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-135754374-null-null.142^v100^pc_search_result_base2&utm_term=docker%E5%A6%82%E4%BD%95%E5%B0%86%E9%95%9C%E5%83%8F%E5%AD%98%E5%82%A8%E5%88%B0github&spm=1018.2226.3001.4187)
