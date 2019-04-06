# Image
## Configuration
- `/etc/docker/daemon.json`：set default image register (no need to do)

        {
          "registry-mirrors": ["https://10.123.97.147"],  
          "max-concurrent-downloads": 6,
          "insecure-registries" : ["docker-registry.xxx.com"] 
        }
    


## basic manipulation
- `docker image ls`: list all images in the local registry
  - `docker image ls -q`: display only image ID 
- `docker search ubuntu:xenial`: search all images from the remote registry
- docker image pull <repository>:<tag>`: download an image from the remote registry to the local registry
  - `docker image pull <repository>`: if we don't specify an image tag, Docker uses `latest` as default tag
  - `docker image pull -a <repository>`: download all the images of the repo  
  - `docker image pull gcr.io/nigelpoulton/tu-demo:v2`: download from a third-party registry
- `docker image inspect ubuntu:xenial`: inspect a local image
- `docker image rm IMG_ID`: remove a local image
  - `docker image rm $(docker image ls -q) -f`: delete all images on ths host
- `docker history IMG_ID`: display all the layers of an image


## tag
- `docker image tag old_repo:old_tag new_repo:new_tag`: change the tag of a local


## create/commit/push
- `docker container commit -m <comment> -a <author> CT_ID REPO:TAG`: create an image from a running container
- push to a remote registry
  - `docker login`: login to `hub.docker.com`
  - `docker image push wukongsun/xenial:net`: upload to the remote registry 


## import/export
- `docker save REPO:Tag > /tmp/registry.tar`: export the registry image
- `docker load < registry.tar`: import the registry image


## TP
### Download a MySQL image
- `docker image ls`
- `docker search mysql`
- `docker pull mysql`
- `docker image ls`
- `docker ps -a`

### Create a Ubuntu:Xenial Image with ifconfig
- `docker container run -it --rm ubuntu:16.04 /bin/bash`
- in this container terminal, run:
  - `ping 8.8.8.8`: it doesn't work since it doesn't have the `ping` tool
  - `apt update`
  - `apt install iputils-ping`
  - `ping 8.8.8.8`: it works now!
- from another terminal, run:
  - `docker container ps`, where you can find `CT_ID`
  - `ddocker container commit -m "xenial with ping" -a "USER_NAME" CT_ID REPO/xenial:net`
  - `docker login`
  - `docker image push REPO/xenial:net`
