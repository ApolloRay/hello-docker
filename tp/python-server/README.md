# Python Web Server
## mysql
- `docker network create python-server`: create a backend network
- `docker volume create mysql`: create a volume
- `docker image pull mysql:5.6`
- `docker container run --name mysql -d --net python-server -v mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=P@ssw0rd  mysql:5.7`
- `mysql -h MYSQL_IP -u root -p`: test the access to the mysql server


## Python Server
### Build python-server Docker Image
- `cd docker`
- `docker build -t python-server:0.1 .`
- `docker image list`: check

### Launch Python Server
- `docker container run --name python-server -d --net python-server -p 6666:8888 python-server:0.1`: use default env
- `docker container run --name python-server -d --net python-server -p 6666:8888 -e MYSQL_HOST=mysql python-server:0.1`: use new env

<!--
## docker-compose Deployment
- `docker-compose up` 
-->

## Test
### Init MySql 
- `mysql -h MYSQL_IP -u root -p < db1_tbl1.sql`: init the db1 database of mysql

### check
- `curl localhost:6666`