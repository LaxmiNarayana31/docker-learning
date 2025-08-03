# Dockerfile ---> Docker image ----> Docker Container

## Basic Docker Commands

```sh
docker pull <image-name>          # pull an image from docker hub
docker ps                         # list running Docker containers
docker ps -a                      # see all containers, including stopped ones
docker images                     # see all images available
docker run <image-name/image-id>  # run a docker image
docker stop <container-id>        # stop a running container
docker start <container-id>       # start a container
```

## To run a docker container

```dockerfile
CMD ["python", "main.py"]
```
CMD: This can be overridden during `docker run`.

```dockerfile
ENTRYPOINT ["python", "main.py"]
```

ENTRYPOINT: This can't be overridden.

```sh
docker build -t <image-name> .    # build the image from Dockerfile (-t: tag name, .: working directory) You can give any name to the image. 
```

To run a web app:

```sh
docker run -d -p <host_port>:<container_port>   # -d: run in background, -p: publish
docker run -p 80:80
```

If any issue with container, you can see the logs by using below command:

```sh
docker logs <container_id>
```

To see real-time logs of your app container:

```sh
docker attach <container_id>
```

To see inside your container:

```sh
docker exec -it <container_id> bash
```

To run a container continuously:

```sh
docker run -itd ubuntu   # -it: interactive mode, -d: detached mode
```

---

## Docker Networks

When you run two containers (e.g., Flask and MySQL), they are independent and can't talk to each other by default. To connect them, use Docker networks.

There are 7 types:

- Host
- Bridge (Default)
- User defined bridge (Custom bridge)
- None
- MACVLAN (Docker Swarm)
- IPVLAN
- Overlay

To see the networks:

```sh
docker network ls
```

To create your own network:
You can give any name to your network name.
```sh
docker network create <network-name> -d bridge
```

### Example: 2-Tier Application (Web + MySQL)
Means one container for application and another one for MySQL DB.
1. Build the image for web-app, then run it. Start the MySQL DB image in a container.

```sh
docker run -d -p 5000:5000 -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=laxmi123 -e MYSQL_DB=testdb flask-app-backend:latest
```

Here `mysql` is the container name, `-d` for detached mode, `-p` for port mapping, `-e` to pass environment variables, `flask-app-backend` is image name, `latest` is tag name. If your container does not appear with `docker ps`, it means it starts and then exits immediately.

After this, the app does not run because the DB and web-app containers are not in the same network.

To solve this, create a network:

```sh
docker network create flask-app-backend -d bridge
```

`flask-app-backend` is the network name.

Then run:

```sh
docker run -d --name mysql --network flask-app-backend -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=testdb mysql
```

Then run the web app:

```sh
docker run -d -p 5000:5000 --network flask-app-backend -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=laxmi123 -e MYSQL_DB=testdb flask-app-backend:latest
```

To inspect a network:

```sh
docker network inspect <network-name>
```

To restart a container:

```sh
docker restart <docker_id>
```

---

## Docker Volume and Storage

Whenever your docker container crashes or is deleted, all data is lost. For example, if you run a MySQL container and it crashes, all data inside that MySQL database is deleted. To prevent this, use Docker volumes to persist data.

Bind the data in the MySQL DB container with the host file system (volume):

```sh
docker volume ls                      # see all existing volumes
docker volume create mysql-data       # create a volume (mysql-data is the folder name)
docker inspect mysql-data             # see the path
```

Then bind the MySQL container with the flask-app-backend:

```sh
docker run -d --name mysql --network flask-app-backend -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=testdb mysql
```

In this case, data is not deleted from MySQL DB even if the container is crashed or deleted.

---

## Docker Compose

Docker Compose is a tool to automate processes. It uses a configuration file (`.yml` or `.yaml`).

Benefits: Automate what you previously did with `docker run`, `build`, `docker volume` in a single file.

You can make multiple docker containers in `docker-compose.yml` (see attached file for demo).

You have to separately install the Docker Compose tool.

To run the docker compose file:

```sh
docker compose up
```

This builds and runs the containers. But you have to first start MySQL; in the service section of docker compose, use `depends_on`.

MySQL starts, but it takes some time to be fully ready for connections. For this, set up a healthcheck.

To run the containers in background (detached mode):

```sh
docker compose up -d
```

## Cleaning Up Docker Resources

To delete unused things like unused containers, images, volumes:

```sh
docker system prune
```

To remove images:

```shl
docker rmi <image_ids>   # rmi means Remove images
```

Suppose you have 500 images, then manually it takes a lot of time. Use:

```sh
docker rmi -f $(docker images -aq)
```

In this command:

- `docker images -aq` gets all image IDs
- `docker rmi -f` removes all images

To remove stopped containers:

```sh
docker compose down
```

This stops running containers and removes them.

To build docker images again:

```sh
docker compose up -d --build
```

This pulls the images and builds things.

---

## Docker Registry

Login first if you are not logged in:

```sh
docker login
```

To push an image to Docker Hub:

```sh
docker image tag <local_image_name>:latest <docker_user_name>/<image_name>:latest
# Example:
docker image tag backend-flask-app:latest LaxmiNarayana31/backend-flask-app:latest
```

Then push to the registry:

```sh
docker push <docker_user_name>/<image_name>:latest
```

After that, you can change your docker compose file to pull the image from Docker Hub registry instead of building it repeatedly:

```yaml
flask_app:
  image: LaxmiNarayana31/backend-flask-app:latest
  container_name: flask_app_container
  environment:
    MYSQL_HOST: mysql
    MYSQL_DATABASE: testdb
    MYSQL_USER: user
    MYSQL_PASSWORD: laxmi12*
  networks:
    - my_network
  ports:
    - "5000:5000"
  restart: always
  depends_on:
    - mysql
  healthcheck:
    test: ["CMD-SHELL", "curl -f http://localhost:5000/health || exit"]
    interval: 10s
    timeout: 30s
    retries: 5
    start_period: 30s
```

---

# Multistage Docker Builds

Image build with Dockerfile:
In every Dockerfile there is a base image. Suppose it is Python, then itself is a big image. So when you build a container it takes a lot of time.

To reduce its size, use multistage Docker build:

**Stage 1: base image 994mb ~ 1.04 GB**

```dockerfile
FROM python:3.7 AS builder

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt
```

---

**Stage 2: base image ~ 125 Mb**

```dockerfile
FROM python:3.7-slim

WORKDIR /app

COPY --from=builder /usr/loal/lib/python3.7/site-packages/ /usr/local/lib/python3.7/site-packages/

COPY . .

ENTRYPOINT ["python", "run.py"]
```

---

Then build the image:

```sh
docker build -t flask-app-mini .
```

Then run:

```sh
docker images
```

You can see the image size.

To drop the logs in a file:

```sh
nohup docker attach <container_id> &
```

---

## Docker in Production

We generally don't use docker containers individually in production.

**Kubernetes**

- Pods: These are things in which docker containers run
- Deployment: Collection of pods (replica)
- Service: Connects the deployment to users
- Ingress: Routing
