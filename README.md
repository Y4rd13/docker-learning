# Docker Course

<a href="https://www.youtube.com/watch?v=fqMOX6JJhGo&ab_channel=freeCodeCamp.org">>> video of the course</a>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#getting-started">Getting Started</a></li>
    <li><a href="#install-docker">Install Docker</a></li>
    <li><a href="#docker-commands">Docker commands</a></li>
    <li><a href="#labs">Labs</a></li>
    <li><a href="#run">Run</a></li>
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
