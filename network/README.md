# Network
## Drivers
- bridge: 
- host: 
- overlay: 

## Intra-Host Network
- `docker network list`: list
- `docker network inspect NET_ID`: show detailed information
- `docker network create NET_ID`: create
  - `docker network create -d DRIVER NET_ID`: specify the network driver to use, by default Bridge
- `docker network rm NET_ID`: remove
- `docker container run --name ct1 -it --rm --net=NET_ID ubuntu:xenial`: launch a CT in a network
- `docker network connect NET_ID CT_ID`: connect a CT to a network, one CT can be connected to multiple networks
- `docker network disconnect NET_ID CT_ID`: disconnect

## TP: VM-VM Ping
- `docker network create net1`
- `docker container run --name ct1 -it --rm --net=net1 wukongsun/xenial:net`
- `docker container run --name ct2 -it --rm --net=net1 wukongsun/xenial:net`
- in ct1: ping ct2


## Inter-Host Network
### Overlay
on the Swarm manager
- `docker network create -d overlay NET_ID`: create the overlay network
- `docker service create --name test --network NET_ID --replicas 2 ubuntu sleep infinity`: attach a service to the net  

## TP: Inter-VM Communication
- `docker network create net1`
- `docker container run --name ct1 -it -d --net=net1 ubuntu:xenial`
- `docker container run --name ct2 -it --net=net1 ubuntu:xenial /bin/bash`
- in the container `ct2`: 
    - `apt update`
    - `apt install iputils-ping`
    - `ping ct1`