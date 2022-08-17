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
