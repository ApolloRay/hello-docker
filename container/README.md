# Container
## ps
- `docker ps`
  - `docker ps -a`: list all the containers included the killed

## run
### run
- `docker container run ubuntu:xenial /bin/bash`: tell Docker which process to run inside container to replace default CMD 
- `docker container run --name CT_Name ubuntu:xenial`: name of the container
- `docker container run -it ubuntu:xenial`: interactive mode, connect your terminal to the CT's bash shell
  - `Ctrl-PQ`: exist and suspend the container 
- `docker container run -it -d ubuntu:xenial`: detached mode (executing as daemon in bg)
- `docker container run -it --rm ubuntu:xenial`: remove after the execution
- `docker container run -d -p 8080:8080 test:latest`: NAT the port
- `docker container run -d -P training/webapp python app.py`: NAT port of the container to a random port of the host

### Resource Limitation
- `docker run -m 200M --memory-swap=300M ubuntu`
  - `-m 200M`: memory
  - `--memory-swap 300M`: memory+swap
- `docker run -it -m 200M --memory-swap=300M progrium/streee --vm 1 --vm-bytes 280M`
  - `--vm 1`: 1 process for the container
  - `--vm-bytes 280M`: 280M memory for the process
- `docker run -c 1024 ubuntu`
  - `-c 1024`: CPU priority 
- `docker run -it --blkio-weight 600`
  - `--blkio-weight 600`: disk input/output priority


## attach/exec
- `docker attach`: attach to the container's terminal
  - `docker attach UUID`
- `docker exec`: run a new process inside the container
  - `docker exec –it CT_ID /bin/bash`: here it attaches a running container with a bash


## stop/kill/start/restart
- `docker container start CT_ID`: restart
- `docker container stop CT_ID`: stop (send SIGTERM + SIGKILL)
- `docker container kill CT_ID`: kill (send SIGKILL)


## pause/unpause
- `docker pause CT_ID`
- `docker unpause CT_ID`


## rm
- `docker container rm CT_ID`: remove a *stopped* container
  - `docker container rm -f CT_ID`: force mode, remove a *running* container
  - `docker container rm -f $(docker container ps -aq)`: remove all the containers


## monitor
- `docker container ps`
- `docker container top CT_ID`
- `docker container top`: real-time monitor
- `docker logs CT_ID`
  - `docker logs -f CT_ID`: continue to display new logs 


## Example
### Manipulation
- `docker container run hello-world`
- `docker container ps`: we can't see the container `hello-world`
- `docker container ps -a`: we can see all the containers including the stopped containers
- `docker container run -it --rm ubuntu:xenial /bin/bash` 
- from another terminal `docker container ps`: what's the difference between the previous case? Why?
- in the container
  - `ps aux`
  - `exit` or `Ctrl-PQ`: exit the container
  - `docker container ps -a`
  - `docker container exec -it CT_ID /bin/bash  `

### Web Server
- `docker container run -it --rm -p 8888:80 ubuntu:xenial`
- install and launch apache2 in the container
    - `apt update`
    - `apt install apache2 vim`
    - `vim /var/www/html/index.html`
    - `apache2ctl -D FOREGROUND`
- access the web page from localhost:8888

