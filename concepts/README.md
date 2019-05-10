# Docker Concepts
## Introduction
### VM vs. Docker
![VM vs. Docker](/Users/ruan/workspace/hello-docker/figures/container-vm.png)


## Docker Engine Components
![Docker Main Components](/Users/ruan/workspace/hello-docker/figures/docker-architecture.png)

- Docker client: send commands
- Docker Daemon: server to handle requests
  - `/etc/systemd/system/multi-user.target.wants/docker.serivce` `-H tcp://0.0.0.0`: configuration to accept remote requests (no need to do)
  - `systemctl daemon-reload` and `systemctl restart docker.service`
  - `docker -H 192.168.88.8 info`: example (no need to do)
- Registry: host Docker images


## Terminology
- image: a lightweight executable package that includes everything needed to run a piece of software, including the code, a runtime, libraries, environment variables, and config files.
  - *image name* = *repository* + *tag*
- container: a runtime instance of an image -- what the image becomes in memory when actually executed. It runs completely isolated from the host environment by default, only accessing host files and ports if configured to do so.
- registry: image store


## Conception
一个程序运起来后的计算机执行环境的总和（内存中的数据、寄存器里的值、堆栈中的指令、被打开的文件，以及各种设备的状态信息的一个集合）被称为一个进程。
容器技术的核心功能，就是通过约束和修改进程的动态表现，从而为其创造出一个“边界”。 
对于Docker等大多数Linux容器来说，Cgroups技术是用来制造约束的主要手段，而Namespace技术则是用来修改进程视图的主要方法。

### Namespace

### Cgroups
               