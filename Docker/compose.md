#### [Back](./README.md)

# Docker Compose

* ### Check Docker Compose Version
```shell
docker-compose version
```

* ### Docker Compose Build
```shell
docker-compose build
```
The build command builds or rebuilds the images in the docker-compose YAML file and creates the containers for your service.

* ### Docker Compose Run
```shell
docker-compose run
```
The run command starts up your services as specified in the docker-compose file by creating the containers from the Docker images.

* ### Docker Compose images
```shell
docker-compose images
```
The images command lets you view a list of the images built from your docker-compose file.

* ### Docker Compose up
```shell
docker-compose up
```
The up command is the combination of the build and run commands.

* ### Docker Compose ps
```shell
docker-compose ps
```
List of all Containers created by docker file.

* ### Docker Compose down
```shell
docker-compose down
```
The down command stops and cleans up containers and images associated with the docker-compose file.

* ### Docker Compose Stop
```shell
docker-compose stop
```
You’ll find the stop command useful if you only want to stop all containers and services in your docker-compose file.