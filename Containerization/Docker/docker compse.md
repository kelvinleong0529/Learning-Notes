
# **YAML file**
- parsing YAML files is slower than parsing JSON files, hence it is not used all the time, because parser doesnt know whether is it reading string or number, it needs to read everthing and try to evaluate it
- YAML files is used for configuration files, and JSON is used for exchanging data
```yaml
---
course_name: Docker Learning Notes
# below is an array
tags:
    - software
    - devops
# below is an object
author:
    name: Kelvin Leong
    age: 24
```

# **Docker Running Modes**
1. run docker -it: (**interactive** mode) means we can execute commands inside the container while running
2. run docker -d: (**detahced** mode) means running the docker in the background of the terminal

# **Docker Volumes**
- dokcer volumes are used for data persistence (databases or stateful applications)
- if we have a database container that runs on the host, if we removed, stop or restart the container then the data in the virtual file system (file system in guest OS, container runs in guest OS, guest OS runs in host OS) will be gone
- we need to **plug** (mount) the host file system to the virtual file system of the container, any changes to the virtual file system will get reflected in the host file system as well and vice-versa
```cmd
docker run -v <host directory>:<container directory>
# run -v means (volume) define the volume connection
```

# **Docker Port Binding**
- we need to link container's port to our host OS port in order to "communicate"
```cmd
docker run -p <host-port>:<container-port> <image-name>
```

# **Docker Environment**
- we can inject environment variables into docker containers
```
docker run -e <name-of-injected-variable>=<value-of-injected-variable>
eg: docker run -e MODE=test
# the value of the variable "MODE" is "test" inside the container
```

# **Docker Compose**
- a tool that help define and share multi-container applications, used to manage several containers
- need to configrued a "docker-compose.yaml" file for docker compose
- we are telling docker how to build images for each services and how to run them
```yaml
---
version: "3.8" # version of the docker compose that we are using
# the names below are arbitary, we can name it as we like
services:
    frontend:
        build: ./frontend # specify how to build the image for front-end services
        ports:
            # map port 3000 of host to port 3000 of container
            - 3000:3000
    backend:
        build: ./backend
        ports:
            - 3001:3001
    database:
        image: mongo:4.0-xenial
        ports:
            - 27017:27017
        volumes:
        - vidly:/data/db

volumes:
    - vidly
```

```
docker-compose up 
// build docker compose based on docker-compose.yaml

docker-compose down 
// stop the compose docker and remove the container

docker-compose up --build -d 
// 'build' is to check if any files has changed
// if detect any changes rebuild the container
// '-d' is to run in detached mode
```
# **Docker Networking**
- by default compose sets up a single network for the app, each container for a service joins the default network and is both **reachable** by the other containers on that network
```yaml
version: "3.9"
services:
  web:
    build: .
    ports:
      - "8000:8000"
  db:
    image: postgres
    ports:
      - "8001:5432"

# A network called myapp_default is created.
# A container is created using web’s configuration. It joins the network myapp_default under the name web.
# A container is created using db’s configuration. It joins the network myapp_default under the name db.
```
- **HOST_PORT** and **CONTAINER__PORT**, in the example above, for **db**, the **HOST_PORT** is 8001 and the container port is 5432 (postgres default). Networked service-to-service communication uses the **CONTAINER_PORT**. When **HOST_PORT** is defined, the service is accessible outside the swarm as well.

# **Docker Links**
- links allow us to define extra aliases by which a service is reachable from another service
```yaml
version: "3.9"
services:

  web:
    build: .
    links:
      - "db:database"
  db:
    image: postgres

# 'db' is reachable at the hostnames 'db' & 'database'
```

# **Docker Expose & ports**
- **expose** allow us to expose a container (service) ports without publishing them or binding them to the host ports (eg: ports are not exposed to host machines, only exposed to other services/containers)
- **ports** allow us to specifiy both host and container port numbers, and share the ports among other services and exposed to the host machine to a random or given port