# WordPress Deployment
In order to deploy a *wordpress* application, we should:
- create 1 network
- create 2 volumes
  - 1 for wordpress
  - 1 for mysql
- create 2 containers
  - 1 for wordpress
  - 1 for mysql

## Network Creation
- `docker network create wordpress`
- `docker network list`

## Volume Creation
- `docker volume create wordpress`
- `docker volume create mysql`
- `docker volume list`

## WordPress Image
- `docker image pull wordpress`
- `docker image inspect wordpress:latest`

## MySql Image
- `docker image pull mysql`
- `docker image inspect mysql:latest`

## Launch Containers
- `docker container run --name mysql -d --net wordpress -v mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=password  mysql:latest`
- `docker container run --name wordpress -d --net wordpress -p 8090:80 --link mysql:mysql -v wordpress:/var/www/html -e WORDPRESS_DB_PASSWORD=password wordpress:latest`
