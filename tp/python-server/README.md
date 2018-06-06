# Python Web Server
## mysql
- `docker network create net_python-server`: create a backend network
- `docker volume create vol_mysql`: create a volume
- `docker image pull mysql:5.6`
- `docker container run --name ct-mysql -d --net net_python-server -v vol_mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=P@ssw0rd  mysql:5.6`
- `mysql -h CT_MYSQL_IP -u root -p`: test the access to the mysql server
- `mysql -h CT_MYSQL_IP -u root -p < db1_tbl1.sql`: init the db1 database of mysql


## Python Server
### Build python-server Docker Image
- `cd docker`
- `docker build -t img-python-server:0.1 .`
- `docker image list`: check

### Launch Python Server
- `docker container run --name ct-python-server -d --net net_python-server -p 8888:8888 img-python-server:0.1`: use default env
- `docker container run --name ct-python-server -d --net net_python-server -p 8888:8888 -e MYSQL_HOST=ct-mysql img-python-server:0.1`: use new env


## Test
- `curl localhost:8888`