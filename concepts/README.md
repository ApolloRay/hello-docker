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