# Docker Basic Commands with Examples

This guide covers essential Docker commands, grouped by category, with descriptions and usage examples.

---

## Docker Lifecycle Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker create`        | Create a new container               | `docker create ubuntu`                  |
| `docker run`           | Run a container from an image        | `docker run -it ubuntu /bin/bash`       |
| `docker pause`         | Pause all processes in a container   | `docker pause <container-id>`           |
| `docker unpause`       | Resume a paused container            | `docker unpause <container-id>`         |
| `docker stop`          | Stop a running container             | `docker stop <container-id>`            |
| `docker start`         | Start a stopped container            | `docker start <container-id>`           |
| `docker restart`       | Restart a container                  | `docker restart <container-id>`         |
| `docker attach`        | Attach to a running container        | `docker attach <container-id>`          |
| `docker wait`          | Wait for container to stop           | `docker wait <container-id>`            |
| `docker rm`            | Remove a container                   | `docker rm <container-id>`              |
| `docker kill`          | Kill a running container             | `docker kill <container-id>`            |

---

## Docker Basic Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker`               | List all available Docker commands    | `docker`                                |
| `docker version`       | Show Docker version info              | `docker version`                        |
| `docker info`          | Display system-wide Docker info       | `docker info`                           |
| `docker pull`          | Pull an image from Docker Hub         | `docker pull ubuntu`                    |
| `docker build`         | Build an image from a Dockerfile      | `docker build .`                        |
| `docker run`           | Run a container from an image         | `docker run -it ubuntu /bin/bash`       |
| `docker commit`        | Create a new image from a container   | `docker commit <container-id> new-image`|
| `docker ps`            | List running containers               | `docker ps`                             |
| `docker ps -a`         | List all containers                   | `docker ps -a`                          |
| `docker start`         | Start a container                     | `docker start <container-id>`           |
| `docker stop`          | Stop a container                      | `docker stop <container-id>`            |
| `docker logs`          | View container logs                   | `docker logs <container-id>`            |
| `docker rename`        | Rename a container                    | `docker rename old_name new_name`       |
| `docker rm`            | Remove a container                    | `docker rm <container-id>`              |
| `docker rmi`           | Remove an image                       | `docker rmi <image-id>`                 |

---

## Docker Image Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker build`         | Build image from Dockerfile           | `docker build -t myimage:1.0 .`         |
| `docker pull`          | Pull image from registry              | `docker pull ubuntu`                    |
| `docker tag`           | Tag an image                          | `docker tag ubuntu myrepo/ubuntu:latest`|
| `docker images`        | List images                           | `docker images`                         |
| `docker push`          | Push image to registry                | `docker push myrepo/ubuntu:latest`      |
| `docker history`       | Show image history                    | `docker history ubuntu`                 |
| `docker inspect`       | Inspect image details                 | `docker inspect ubuntu`                 |
| `docker save`          | Save image to tar archive             | `docker save ubuntu > ubuntu.tar`       |
| `docker import`        | Import image from tarball             | `docker import ubuntu.tar ubuntu:latest`|
| `docker export`        | Export container to tar               | `docker export <container-id> > container.tar`|
| `docker load`          | Load image from tar archive           | `docker load < ubuntu.tar`              |
| `docker rmi`           | Remove image                          | `docker rmi ubuntu`                     |
| `docker system prune`  | Remove unused data                    | `docker system prune`                   |

---

## Docker Container Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker start`         | Start a container                     | `docker start <container-id>`           |
| `docker stop`          | Stop a container                      | `docker stop <container-id>`            |
| `docker restart`       | Restart a container                   | `docker restart <container-id>`         |
| `docker pause`         | Pause a container                     | `docker pause <container-id>`           |
| `docker unpause`       | Unpause a container                   | `docker unpause <container-id>`         |
| `docker run`           | Run a new container                   | `docker run -it ubuntu`                 |
| `docker ps`            | List containers                       | `docker ps`                             |
| `docker exec`          | Run command in running container      | `docker exec -it <container-id> /bin/bash`|
| `docker logs`          | View container logs                   | `docker logs <container-id>`            |
| `docker rename`        | Rename a container                    | `docker rename old_name new_name`       |
| `docker rm`            | Remove a container                    | `docker rm <container-id>`              |
| `docker inspect`       | Inspect container details             | `docker inspect <container-id>`         |
| `docker attach`        | Attach to running container           | `docker attach <container-id>`          |
| `docker kill`          | Kill a running container              | `docker kill <container-id>`            |
| `docker cp`            | Copy files between host and container | `docker cp <container-id>:/path /host/path`|

---

## Docker Compose Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker-compose build` | Build images defined in compose file  | `docker-compose build`                  |
| `docker-compose up`    | Create and start containers           | `docker-compose up -d`                  |
| `docker-compose ps`    | List containers                       | `docker-compose ps`                     |
| `docker-compose start` | Start existing containers             | `docker-compose start`                  |
| `docker-compose run`   | Run a one-off command                 | `docker-compose run app`                |
| `docker-compose rm`    | Remove stopped containers             | `docker-compose rm -f`                  |
| `docker-compose stop`  | Stop running containers               | `docker-compose stop`                   |

---

## Docker Volume Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker volume create` | Create a volume                       | `docker volume create myvolume`         |
| `docker volume inspect`| Inspect a volume                      | `docker volume inspect myvolume`        |
| `docker volume rm`     | Remove a volume                       | `docker volume rm myvolume`             |
| `docker volume prune`  | Remove all unused volumes             | `docker volume prune`                   |

---

## Docker Networking Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker network create`| Create a network                      | `docker network create mynetwork`       |
| `docker network ls`    | List networks                         | `docker network ls`                     |
| `docker network inspect`| Inspect a network                    | `docker network inspect mynetwork`      |
| `docker network prune` | Remove unused networks                | `docker network prune`                  |

---

## Docker Logs & Monitoring Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker ps -a`         | List all containers                   | `docker ps -a`                          |
| `docker logs`          | Show container logs                   | `docker logs <container-id>`            |
| `docker events`        | Show container events                 | `docker events`                         |
| `docker top`           | Show running processes in container   | `docker top <container-id>`             |
| `docker stats`         | Show resource usage                   | `docker stats <container-id>`           |
| `docker port`          | Show container's public ports         | `docker port <container-id>`            |

---

## Docker Prune Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker system prune`  | Remove unused data                    | `docker system prune`                   |
| `docker system prune -a`| Remove all unused images             | `docker system prune -a`                |
| `docker image prune`   | Remove unused images                  | `docker image prune`                    |
| `docker container prune`| Remove unused containers             | `docker container prune`                |
| `docker volume prune`  | Remove unused volumes                 | `docker volume prune`                   |
| `docker network prune` | Remove unused networks                | `docker network prune`                  |

---

## Docker Hub Commands

| Command                | Description                          | Example                                 |
|------------------------|--------------------------------------|-----------------------------------------|
| `docker search`        | Search for images on Docker Hub       | `docker search ubuntu`                  |
| `docker pull`          | Pull image from Docker Hub            | `docker pull ubuntu`                    |
| `docker login`         | Login to Docker Hub                   | `docker login`                          |
| `docker push`          | Push image to Docker Hub              | `docker push myimage`                   |
| `docker logout`        | Logout from Docker Hub                | `docker logout`                         |

---

> For more details, refer to the official Docker documentation: [https://docs.docker.com/](https://docs.docker.com/)