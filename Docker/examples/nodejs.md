#### [Back](../example.md)

# NodeJS on Ubuntu

## Command to build
```bash
docker compose build
```

## Command to run docker
```bash
docker compose up -d
```

## Docker File
```bash
FROM ubuntu:latest
RUN apt-get update 

RUN apt-get install -y apache2 vim \
        nodejs \
        npm \
        curl 

RUN apt-get clean

RUN npm install -g @loopback/cli
CMD /bin/bash
```

## Compose File
```yaml
services:
  docker-node:
    build: .
    image: sfvishalgupta/docker-node
    container_name: docker-node
    restart: unless-stopped
    working_dir: /var/www/src
    command: ["/bin/bash"]
    stdin_open: true 
    tty: true
    volumes:
      - ./src:/var/www/src
  
```

## Go to Docker Container
```bash
docker exec -it docker-node bash
```