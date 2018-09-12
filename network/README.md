# Network
## Intra-Host Network
### None
- `docker run -it --network=nene busybox`: no network stack

### Bridge
- `docker network list`: list
- `docker network inspect NET_ID`: show detailed information
- `docker network create NET_ID`: create
  - `docker network create -d DRIVER NET_ID`: specify the network driver to use, by default Bridge
- `docker network rm NET_ID`: remove
- `docker container run --name ct1 -it --rm --net=NET_ID ubuntu:xenial`: launch a CT in a network
- `docker network connect NET_ID CT_ID`: connect a CT to a network, one CT can be connected to multiple networks
- `docker network disconnect NET_ID CT_ID`: disconnect

### Host
- `docker run -it --network=host busybox`: container and host share the same network stack
  - performance 
  - use the container to config the host network stack


## User-defined Network
### bridge
- `docker network create --driver bridge --subnet 172.88.88.0/24 --gateway 172.88.88.1 NET_ID`
- `docker run -it --network=NET_ID busybox`
- `docker run -it --network=NET_ID --ip 172.88.88.88 busybox`

### joined
- `docker run -d -it --name=CT_ID httpd`
- `docker run -d -it --network=container:CT_ID busybox`: the containers share the same network stack

### DNS
- `docker run -it --network=NET_ID --name CT_ID busybox`
  - `ping -c 3 CT_ID2`
 

## Example
### VM-VM Ping
- `docker network create net1`
- `docker container run --name ct1 -it --rm --net=net1 wukongsun/xenial:net`
- `docker container run --name ct2 -it --rm --net=net1 wukongsun/xenial:net`
- in ct1: ping ct2

### Inter-VM Communication
- `docker network create net1`
- `docker container run --name ct1 -it -d --net=net1 ubuntu:xenial`
- `docker container run --name ct2 -it --net=net1 ubuntu:xenial /bin/bash`
- in the container `ct2`: 
    - `apt update`
    - `apt install iputils-ping`
    - `ping ct1`