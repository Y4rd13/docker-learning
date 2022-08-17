# Docker Course

<a href="https://www.youtube.com/watch?v=fqMOX6JJhGo&ab_channel=freeCodeCamp.org">>> video of the course <<<</a>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#getting-started">Getting Started</a></li>
    <li><a href="#install-docker">Install Docker</a></li>
    <ul>
        <li><a href="#popular-docker-images">Popular docker images</a></li>
    </ul>
    <li><a href="#docker-commands">Docker Commands</a></li>
    <li><a href="#docker-run">Docker Run</a></li>
    <ul>
        <li><a href="#run--port-mapping">RUN -PORT MAPPING</a></li>
        <li><a href="#run--volume-mapping">RUN -VOLUME MAPPING</a></li>
        <li><a href="#inspect-container">Inspect Container</a></li>
        <li><a href="#container-logs">Container Logs</a></li>
    </ul>
    <li><a href="#enviroment-variables">Enviroment Variables</a></li>
    <li><a href="#images">Images</a></li>
    <li><a href="#cmd-vs-entrypoint">CMD vs ENTRYPOINT</a></li>
    <li><a href="#networking">Networking</a></li>
    <li><a href="#storage">Storage</a></li>
    <li><a href="#compose">Compose</a></li>
    <li><a href="#registry">Registry</a></li>
    <li><a href="#engine">Engine</a></li>
    <li><a href="#docker-on-windows">Docker on Windows</a></li>
    <li><a href="#container-orchestration">Container Orchestration</a></li>
    <li><a href="#docker-swarm">Docker Swarm</a></li>
    <li><a href="#kubernetes">Kubernetes</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ol>
</details>
</br>

---

## Getting Started

This is a course on Docker. It is a good way to get started with Docker.

## Install Docker

Got to [Docker Hub](https://docs.docker.com/engine/install/ubuntu/)

Easiest way to install Docker is to use the [Convient Script](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script):

```bash
 curl -fsSL https://get.docker.com -o get-docker.sh
 sudo sh get-docker.sh

 # check version with
 sudo docker --version
```

### Popular docker images

GO to [Docker Hub](https://hub.docker.com/) and search for images.

For example:

```bash
 sudo docker run docker/whalesay cowsay Hello friend!
  _______________
< Hello friend! >
 ---------------
    \
     \
      \
                    ##        .
              ## ## ##       ==
           ## ## ## ##      ===
       /""""""""""""""""___/ ===
  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
       \______ o          __/
        \    \        __/
          \____\______/
```

## Docker Commands

```bash
 docker run # run a container from an image
 docker ps # list all containers
 docker ps -a # list all containers with details
 docker images # list all images
 docker stop <container id> # stop a container
 docker rm <container id> # remove a container
 docker rmi <image id> # remove an image
 docker run <container id> # run a container in the foreground (attach mode)
 docker run -d <image id> # run an image and keep it running in the background (daemon)
 docker run -it <image id> # run an image in the foreground (interactive)
 docker attach <container id> # attach to a container (interactive)
 docker run -P <image id> # run an image and expose a port


 docker exec -it <container id> bash # run a command in the container
    # for example: docker exec -it <container id> bash or docker exec -it <container id> sh my_script.sh
 docker commit <container id> <image id> # commit a container into an image

 docker system prune -a --volumes # remove all unused images and containers
 docker rm -vf $(docker ps -aq)  # remove all containers
 docker rmi -f $(docker images -aq) # remove all images
```

## Docker Run

```bash
# To run another version of a container (i.e. redis) use the following command, else it will be the latest version:
docker run -d --name <container name> <image id>
docker run redis:4.0.14

# Interactive mode (for example, to run a bash shell inside the container):
docker run -it <image id> # `it` stands for `Interactive` mode pseudo `Terminal`
docker run -i <container>/<image>
```

### RUN -PORT MAPPING

To map a port to a container, use the following command:

```bash
docker run -d -p <port>:<port> <image id>
docker run -d -p 80:80 -p 443:443 <image id> # map ports 80 and 443 to the container
docker run -p 80:8000 <container>/<image> # map port 80 to the container on port 8000
```

This way you can run multiple instances of your application and map them to different ports.
You can't map to the same port on the docker host more than once.

```bash
docker run -p 80:8000 django-api/app_1
docker run -p 5000:8000 django-api/app_2
docker run -p 5001:8000 django-api/app_3
docker run -p 6379:6379 redis
docker run -p 3306:3306 mysql
```

### RUN -VOLUME MAPPING

To persist data, map a directory outside the container on the Docker host to a directory inside the container:

- this will mount the external directory to a folder inside the Docker container
- all your data will be stored in the external volume, even if you delete the Docker container

```bash
docker run -v <host path>:<container path> <image id>
docker run -d -v /opt/datadir:/var/lib/mongo mongo:3.4
```

### Inspect Container

```bash
# inspect a container and get details about it
docker inspect <container id>
docker inspect <container name>
```

### Container Logs

```bash
docker logs <container id>
docker logs <container name> # logs for the most recent container
docker logs --follow <container id> # follow the logs of the container
```

# Enviroment Variables

If you want to pass environment variables to your container, use the following command:

```bash
# set an enviroment variable
docker run -e <key>=<value> <image id>
docker run -e <key>=<value> -e <key>=<value> <image id>

# For example
docker run -e APP_MODE=production -e SECRET_KEY=<secret key> django-api/app_1

# multiple env variables
docker run -e <key>=<value> -e <key>=<value> <image id>

# Use insepect to see the env variables
docker inspect <container id>
```

# Docker Images

```bash

```
