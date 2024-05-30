#### [Back](./README.md)

# Docker Commands

* ### Docker Login
```shell
docker login
```

* ### List Docker Images
```shell
docker image ls
docker images
```

* ### Pull Docker Image
```shell
docker pull imageName:tag
```

* ### Docker run interactive
```shell
docker run -ti --rm ubuntu /bin/bash
```
1:- ti is for Interactive terminal mode
2:- /bin/bash is to run bash
3:- --rm instructs docker to automatically remove the docker container after we stop.

* ### Docker run with Port Forwarding
```shell
docker run -d -p 8080:80 nginx
```

* ### Docker with map folder
```shell
sudo docker run -ti --rm -v ~/Docker_Share:/data ubuntu /bin/bash
```

* ### List Docker Container
```shell
docker ps -a
```

* ### Docker save container state
```shell
docker commit -p container_id new_container_name
```

* ### Docker push new Image to registry
```shell
docker image push [OPTIONS] NAME[:TAG]
```
