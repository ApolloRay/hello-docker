# Dockerfile
Dockerfile specifies all the configurations to build an image.

## Instruction
- `FROM`: base image
- `LABEL`: replace the previous MAINTAINER, metadata for the image
- `ENV`: define environment variables to be used by *RUN*, *ENTRYPOINT*, *CMD*
  - `ENV MY_VERSION 1.3`
  - `RUN apt-get install -y mypackage=$MY_VERSION`
- `RUN`: effectuate actions as:  
  - install packages
  - modify configuration
  - create links and directories
  - create users and groups
- `COPY/ADD`: copy files from the host to the container
  - `COPY index.html /var/www/html/index.html`
  - `COPY ["index.html", "/var/www/html/index.html"]`
  - `ADD`: can unzip tar, zip, taz files
- `VOLUME`: create default mount points
  - `VOLUME ["/etc/mysql/mysql.conf.d", "/var/lib/mysql", "/var/log/mysql"]`
- `WORKDIR`: switch path inside the container
- `EXPOSE`: export a TCP port on the container
- `CMD`: command to be run when launch the container
  - if there are multiple CMD, only the last will be run 
  - `docker container run NEW_CMD`: will be replaced by the NEW_CMD
- `ENTRYPOINT`: command always to be run when launch the container, usually to launch a daemon 
  - always run even if add another NEW_CMD
  - `docker container run NEW_CMD`: NEW_CMD will be added as parameters to ENTRYPOINT

- `USER`: execute the commands with which user
- `ONBUILD`:
- `HEALTHCHECK`: 
- `SHELL`: use which shell to execute commands


## Build Image
- `docker image build` create a new image using the instructions in the Dockerfile
  - `docker image build -t apache2-demo:v1 .`: `-t` stands for tag/name 
  - `docker image build -t apache2-demo:v1 -f DockerfileXXX .`: `-f` use a Dockerfile with an arbitrary name
- `docker image history apache2-demo`: show image build history 

## ENV
### Shell Env
- `docker build -t img1 -f Dockerfile-env .`: create the image
- `docker run --name ct1 --rm img1`: see the default msg in default file /tmp/xxx.log
- `docker run --name ct2 --rm -e MSG=111 img1`: see the new msg

### Python Argparse Env
- `docker build -t img1 -f Dockerfile-env-python .`: create the image
- `docker run --name ct1 --rm img1`: see the default msg
- `docker run --name ct2 --rm -e MSG1=aaa -e MSG2=bbb img1`: see the new msgs

### Using the same image to launch different Python scripts
- `docker build -t img1 -f Dockerfile-env-python2 .`: create the image
- `docker run --name ct2 --rm -v $(pwd):/workspace img1`: launch the default script
- `docker run --name ct2 --rm -v $(pwd):/workspace -e APP=/workspace/app2.py img1`: launch the new script


## TP: Apache2 Web Server
- write a Dockerfile to create an image with packages php, apache (apache2, libapache2-mod-php)
- add a index.php file with: `<?php phpinfo() ?>`

See the [Dockerfile](Dockerfile) as the answer
- `docker image build -t apache2-demo .`
- `docker container run -d -p 8885:80 apache2-demo`
- test: 
  - `http://localhost:8885/index.php`: NAT access through browser
  - `http://172.17.0.2:80/index.php`: direct access through browser

