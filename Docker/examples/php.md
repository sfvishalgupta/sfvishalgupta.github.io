#### [Back](../example.md)

# Apache with PHP on Ubuntu

## Command to run docker
```bash
docker compose up -d
```

## Dockerfile
```bash
FROM ubuntu:latest
RUN apt-get update 

RUN apt-get install -y apache2 vim \
        php \
        libapache2-mod-php  \
        php-cli \
        php-cgi \
        php-pgsql \
        curl \
        php-curl

RUN apt-get clean

EXPOSE 80
CMD apachectl -D FOREGROUND
```

## Compose File
```yaml
services:
  kc:
    build: .
    image: sfvishalgupta/kc
    container_name: kc
    restart: unless-stopped
    working_dir: /var/www/html
    volumes:
      - ./KC:/var/www/html
    ports:
      - "8000:80"
    extra_hosts:
      - "host.docker.internal:host-gateway"
    env_file:
      - path: .env # default
        required: true
```