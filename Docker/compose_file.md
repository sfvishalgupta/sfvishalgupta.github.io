#### [Back](./README.md)

# Docker Compose File.

* ### Docker Compose Yaml file example
```yaml
web:
  build: .
  links:
    - "database_default"
  ports:
    - "8000:80"
  volumes:
    - ".:/app:rw"
    - "./data:/data:rw"
  command: python manage.py runserver 0.0.0.0:80
  env_file: .env-local

database_default:
  image: postgres:13.5-alpine
  environment:
    POSTGRES_DB: "db"
    POSTGRES_HOST_AUTH_METHOD: "trust"
    SERVICE_MANAGER: "fsm-postgres"
  volumes:
    - ".:/app:rw"
```
* * **build:** build it from the Dockerfile in the current directory
* * **links:** a link to the database container (database_default)
* * **ports:** map the external port 8000 to the internal port 80
* * **volumes:**
    .:/app:rw maps the parent directory on the host to /app in the container, with read and write access
    /data:/data:rw maps the data directory on the host to /data in the container, with read and write access

* * **command:** by default, when the command docker-compose run is issued, execute python manage.py runserver 0.0.0.0:80 (this will override the CMD instruction in the Dockerfile)

* * **env_file:** use the .env-local to supply environment variables to the container

