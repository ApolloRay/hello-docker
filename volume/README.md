# Volume
## Manipulation
- `docker volume list`: list
- `docker volume inspect VOL_ID`: inspect
- `docker volume create VOL_ID`: create


## Bind Mount
Mount host filesystem to container volume
- `docker container run -it --rm -v VOL_ID:path ubuntu:xenial`: attach a volume to a container
  - `docker container run ... -v $(pwd):path...`: sync local dir to the container
  - `docker container run ... -v $(pwd):path:rw ...`: setup *rw* permission for the volume
  - `docker container run ... -v $(pwd):path:ro ...`: setup *ro* permission for the volume


## Managed Volume
- `docker run -d -p 80:80 -v VOL_ID:/usr/local/apache2/htdocs httpd`
- `docker run -d -p 80:80 -v /usr/local/apache2/htdocs httpd`: a random volume will be created in `/var/lib/docker/volumes/XXX/_data`
  - `echo "xxx" > /var/lib/docker/volumes/XXX/_data`


<!-- ## Volume Container
- `docker create --name vc_data -v ~/xxx:/usr/local/apache2/htdocs busybox`
- `docker run --name web1 -d -p 80 --volume-from vc_data httpd`: separate container from host
-->


## Example
- `docker volume create vol1`
- `docker container run -it --rm -v vol1:/data ubuntu:xenial /bin/bash`
- in the container
  - `ls /data`: check the path in the container
  - `touch /data/xxx`
  - `exit`
- `docker ps`: the container is killed
- `docker container run -it --rm -v vol1:/data ubuntu:xenial /bin/bash`: create a new container
- in the container
  - `ls /data`: check the previously created `xxx` file in the container

