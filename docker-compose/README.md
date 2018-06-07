# docker-compose
Manage several containers at the same time. By default, there is a `docker-compose.yml` file. 

## Installation
```bash
sudo apt-get install python-pip
sudo pip install docker-compose
```

## Build and Run
- `docker-compose up`
- `docker-compose ls`
- `docker-compose up -d`: de-attached mode
- `docker-compose run CT_ID cmd`: execute one cmd in a container
- `docker-compose stop`

## Static Web
- `docker-compose up`
- test: `http://localhost:5000`

## Dynamic Web with Volume
