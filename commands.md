# Docker Commands

Some of the most commonly used docker commands are 

一些最常用的 docker 命令是

## image

```sh
# Lists docker images on the host machine.
docker images
```

### other to image (pull, build)

```sh
# Downloads an image from the configured registry.
docker pull <image_name>
# Builds image from Dockerfile.
docker build -t <image_name> -f <Dockerfile_path> .
```

### image to other (push, save, load, None)

```sh
# Pushes an image to the configured registry.
docker push <image_name>
# Saves an image to a tar file.
docker save -o <tar_file_path> <image_name>
# Loads an image from a tar file.
docker load -i <tar_file_path>
# Removes an image from the host machine.
docker rmi <image_name>
```

### image to container (run(create and start))

**[volumes](volumes.md)**

```sh
# Create a new container from an image with volume mapping.
docker run -v <host_path>:<container_path> <image_name>
```

```sh
# Create a new container from an image.(create and start)
docker run <image_name>
# Create a new container from an image with a name.
docker run --name <container_name> <image_name>
# Create a new container from an image and run in background.
docker run -d <image_name>
# Create a new container from an image with port mapping.
# 访问host_prot时就会访问container_port
docker run -p <host_port>:<container_port> <image_name>
# Create a new container from an image with interactive mode.
docker run -it <image_name> /bin/bash
# Create a new container from an image with interactive mode and run in background.
docker run -dit <image_name> /bin/bash
# Create a new container from an image with environment variables.
docker run -e <key>=<value> <image_name>
# Create a new container from an image with memory limit.
docker run -m <memory_limit> <image_name>
```

当`exit`退出容器时，容器也会停止。

use `docker run --help` to look into more arguments.

```sh
常⽤可选参数说明：
* -i 表示以《交互模式》运⾏容器。
* -t 表示容器启动后会进⼊其命令⾏。加⼊这两个参数后，容器创建就能登录进去。即分配⼀个伪终端。
* --name 为创建的容器命名。
* -v 表示⽬录映射关系，即宿主机⽬录:容器中⽬录。注意:最好做⽬录映射，在宿主机上做修改，然后共享到容器上。
* -d 会创建⼀个守护式容器在后台运⾏(这样创建容器后不会⾃动登录容器)。
* -p 表示端⼝映射，即宿主机端⼝:容器中端⼝。
* --network=host 表示将主机的⽹络环境映射到容器中，使容器的⽹络与主机相同。
```

## container

```sh
# Lists all containers on the host machine.
docker ps -a
# Lists running containers on the host machine.
docker ps
# Stops running container.
docker stop <container_id>
# Stops all running containers.
docker stop $(docker ps -a -q)
# kill a running container.
docker kill <container_id>
# Starts a stopped container.
docker start <container_id>
# Removes a stopped container.
docker rm <container_id>
```

### exec in container

```sh
# Run a command in a running container.
docker exec <container_id> <command>
# Run a command in a running container in interactive mode.
docker exec -it <container_id> /bin/bash
```

### container to image (commit)

```sh
# Create a new image from a container.
docker commit <container_id> <image_name>
```

请注意，`docker commit` 命令只会保存容器的文件系统的当前状态，它不会保存任何关于容器的元数据（如环境变量，暴露的端口，卷等）。如果你想保存这些信息，你应该使用 `Dockerfile` 和 `docker build` 命令来创建你的镜像。

### docker network

Manage Docker networks such as creating and removing networks, and connecting containers to networks.

管理 Docker 网络，例如创建和删除网络，以及将容器连接到网络。
