# Container
## ps
- `docker container ps`
- `docker container ps -a`

## run
- `docker container run ubuntu:xenial`: tell the Docker daemon to start a new container
  - `docker container run ubuntu:xenial /bin/bash`: tell Docker which process to run inside container to replace default CMD 
  - `docker container run --name CT_Name ubuntu:xenial`: name of the container
  - `docker container run -it ubuntu:xenial`: interactive mode, connect your terminal to the CT's bash shell
    - `Ctrl-PQ`: exist and suspend the container 
  - `docker container run -it -d ubuntu:xenial`: detached mode (executing as daemon in bg)
  - `docker container run -it --rm ubuntu:xenial`: remove after the execution
  - `docker container run -d -p 8080:8080 test:latest`: NAT the port
  - `docker container run -d -P training/webapp python app.py`: NAT port of the container to a random port of the host

## exec
run a new process inside the container
- `docker container exec –it CT_ID /bin/bash`: here it attaches a running container with a bash

## stop/kill/start
- `docker container start CT_ID`: restart
- `docker container stop CT_ID`: stop (send SIGTERM + SIGKILL)
- `docker container kill CT_ID`: kill (send SIGKILL)

## rm
- `docker container rm CT_ID`: remove a *stopped* container
  - `docker container rm -f CT_ID`: force mode, remove a *running* container
  - `docker container rm -f $(docker container ps -aq)`: remove all the containers

## TP
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

