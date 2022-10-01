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
    <ul>
        <li><a href="#bridge">Bridge</a></li>
        <li><a href="#none">None</a></li>
        <li><a href="#host">Host</a></li>
        <li><a href="#user--defined networks">User-defined networks</a></li>
        <li><a href="#inspect-network">Inspect Network</a></li>
        <li><a href="#embedded-dns">Embedded DNS</a></li>
    </ul>
    <li><a href="#storage">Storage</a></li>
    <ul>
      <li><a href="#layered-architecture">Layered Architecture</a></li>
      <li><a href="#volumes">Volumes</a></li>
         <ul>
            <li><a href="#named-volumes-/-volume-mounts">Named Volumes / Volume Mounts</a></li>
            <li><a href="#bind-mounts">Bind Mounts</a></li>
         </ul>
      <li><a href="#storage-drivers">Storage Drivers</a></li>
    </ul>
    <li><a href="#docker-compose">Docker Compose</a></li>
    <li><a href="#engine">Engine</a></li>
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

<p align="right">(<a href="#top"> back to top </a>)</p>

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

<p align="right">(<a href="#top"> back to top </a>)</p>

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

<p align="right">(<a href="#top"> back to top </a>)</p>

## Enviroment Variables

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

<p align="right">(<a href="#top"> back to top </a>)</p>

## Docker Images

An example for a simple django API build will be:

```Dockerfile
# INSTRUCTION : ARGUMENT/S
# Start from a base OS or another image
FROM Ubuntu

# Install all dependencies
RUN apt-get update && apt-get install python
RUN pip install django && pip install djangorestframework

# Copy the files from the local system onto the Docker image
# and create a directory for the project
# COPY : CURRENT DIRECTORY : DESTINATION
COPY . /opt/source-code

# Run the project inside the container with the specified environment variables
ENTRYPOINT DJANGO_API=/opt/source-code/manage.py runserver
```

```bash
# Build the image
docker build -t django-api/app_1 .

# # Run the image
# docker run -d -p 80:8000 django-api/app_1
```

To run a Dockerfile, use the following command:

```bash
docker build -t <image name> .
docker build . -f Dockerfile -t <image name>/app_1 # build the image
docker push <image name>/app_1 # push the image to the Docker Hub
```

```

```

In case of failure, you can always rebuild the Dockerfile image.

<p align="right">(<a href="#top"> back to top </a>)</p>

## CMD vs ENTRYPOINT

- **CMD** is the command that is run when the container is started.
- **ENTRYPOINT** is the command that is run when the container is started.

**Differences:**

In the case of the

- **CMD**, the command line parameters passed will get replaced entirely.
- **ENTRYPOINT**, the command line parameters will get appended.

```Dockerfile
# CMD command parameters
CMD ["python", "manage.py", "runserver"]

# or also without an array
CMD python manage.py runserver
```

The **ENTRYPOINT** instruction is used to specify the command that is run when the container is started as an entrypoint:

```Dockerfile
# ENTRYPOINT command parameters
ENTRYPOINT ["python", "manage.py", "runserver"]
```

But also it can be used like this:

```Dockerfile
# Dockerfile
FROM Ubuntu
...
ENTRYPOINT ["sleep"]

# then in out bash
docker run ubuntu-sleeper sleep 10
```

And then we can use both such as:

```Dockerfile
FROM Ubuntu
...
# example 1
ENTRYPOINT ["sleep"]
CMD ["5"]

# You can override it in your terminal
docker run --entrypoint sleep2.0 ubuntu-sleeper 10

# example 2
ENTRYPOINT ["/bin/bash", "-e", "docker-entrypoint.sh"]
CMD python manage.py runserver 0.0.0.0:8000
```

<p align="right">(<a href="#top"> back to top </a>)</p>

## Networking

When you look at networking in Docker, when you install Docker, it created three networks automatically:

`| BRIDGE | NONE | HOST |`

### BRIDGE

`docker run Ubuntu`

Is the default network a container gets attached to.<br/>
It is a private internal network created by Docker on the host,
all containers attached to this network by default, and they get an internal IP address,
usually in the range of `172.17.x.x`.
<br/><br/>
**The containers can access** each other using this **internal IP** if required.
**To access** any of these containers from the outside world, **map the ports** of these containers to the port on the Docker host.

**Another way o access** the containers externally is to associate the container to the host network. This takes out any network isolation between the Docker host and the container. Meaning if you were to run a web server on port 5000. In a web app container, it is automatically as accessible on the same port externally without requiring any port mapping as the web container uses the hosts network.

This will also mean that unlike before,you will now not be able to run multiple web containers on the same host on the same port, as the ports are now common to all containers in the host network.

### NONE

`docker run Ubuntu --network=none`

With the **None** network,the containers are not attached to any network and doesn't have any access to the external network, or other containers. They run in an isolated network.

### HOST

`docker run Ubuntu --network=host`

You can associate the container with any other network, specify the network information, using the network command line parameter like this:

### User-defined networks

```bash
docker network create \
    --driver=bridge \
    --subnet 182.18.0.0/16
    custom-isolated-network
```

We could create our own internal network using the command Docker network, create and specify the driver which is bridge in this case, and the subnet for that network followed by the custom isolated network name.

Run the `docker network ls` command to list all networks.

### Inspect Network

So how do we see the network settings and the IP address assigned to an existing container? Run the `docker inspect <container-name/id>`, and you will find a section on network settings.

There you can see the type of network the container is attached to its internal IP address, MAC address, and other settings.

```bash
[
  {
     "Id":"35505f7810d17291261a43391d4b6c0846594d415ce4f4d0a6ffbf9cc5109048",
     "Name":"/blissful_hopper",
     "NetworkSettings":{
        "Bridge":
        "Gateway":"172.17.0.1",
        "IPAddress":"172.17.0.6",
        "MacAddress":"02:42:ac:11:00:06",
        "Networks":{
           "bridge":{
              "Gateway":"172.17.0.1",
              "IPAddress":"172.17.0.6",
              "MacAddress":"02:42:ac:11:00:06",
           },
        }
     }
  }
]
```

### Embedded DNS

Containers can reach each other using their names.

For example, if you have a web server and a MySQL database container running  
on the same node. How can I get my web server to access the database on the database container?

The right way to do it is to **use the container name**. All containers in a Docker host can resolve each other with the name of the container. Docker has a built in DNS server that helps the containers to resolve each other using the container name.

---

_How does Docker implement networking?_ What's the technology behind it? Like how are the containers isolated within the host?

Docker uses network namespaces that creates a separate namespace for each container.  
It then uses virtual Ethernet pairs to connect containers together.

---

<p align="right">(<a href="#top"> back to top </a>)</p

# Docker Storage

By default docker store its data in `/var/lib/docker` directory.

```
/var/lib/docker/
   aufs/
   containers/
   image/
   volumes/
```

## Layered Architecture

When docker builds images, it uses a layered architecture.
Each line of instruction in the Dockerfile creates a new layer in the Docker image,
with just the changes from the previous layer.

Each layer its reflected in the size of the image.
Docker reuses all the previous layers from cache, and quickly rebuilds the images by updating the latest source code.

## Volumes

see [docker website, volumes](https://docs.docker.com/storage/volumes/)

### Named Volumes / Volume Mounts

Docker volumes are file systems mounted on Docker containers to preserve data generated by the running container.
The volumes are stored on the host, independent of the container life cycle.
This allows users to back up data and share file systems between containers easily.

```bash
docker volume create data_volume

/var/lib/docker/
   volumes/
      data_volumes/
         _data/
```

```
docker run -v data_volume:/var/lib/mysql mysql
```

This will create a new container and mount the `data_volume` at the `/var/lib/mysql` directory inside the container.
Even if the container is destroyed, the data is still active in the volume.

### Bind Mounts

If we would like to store the data in a specific directory on the host, we can use the `-v` option to specify the host directory.

```bash
docker run -v /opt/data:/var/lib/mysql mysql
docker run -v /data/mysql:/var/lib/mysql mysql
docker run -v <host-dir>:<container-dir> <image-name>

# also
docker run \
   --mount type=bind,source=/opt/data,target=/var/lib/mysql
```

The difference between a volume and a bind mount is that volumes are managed by Docker and are located in `/var/lib/docker/volumes/`.
Bind mounts are directories on the host machine that are mounted into the container.
So, if you want to share data between containers, you should use volumes.

see [here](https://youtu.be/fqMOX6JJhGo?t=4500)

## Storage Drivers

The responsible to mantain all this operations are the storage drivers, which enable layers and volumes.
Some of them are:

- AUFS
- ZFS
- BTRFS
- Device mapper
- Overlay
- Overlay2

The selection of the storage driver is done by the docker daemon, and it depends on the host OS.

<p align="right">(<a href="#top"> back to top </a>)</p>

# Docker Compose

see [docker website, compose](https://docs.docker.com/get-started/08_using_compose/#:~:text=Docker%20Compose%20is%20a%20tool,or%20tear%20it%20all%20down.)

Docker Compose is a tool that was developed to help define and share multi-container applications.
With Compose, we can create a YAML file to define the services and with a single command, can spin everything up or tear it all down.

<p align="right">(<a href="#top"> back to top </a>)</p>

## Update docker-compose

https://stackoverflow.com/questions/49839028/how-to-upgrade-docker-compose-to-latest-version

## Install latest docker-compose

```bash
VERSION=$(curl --silent https://api.github.com/repos/docker/compose/releases/latest | grep -Po '"tag_name": "\K.*\d')
DESTINATION=/usr/local/bin/docker-compose
sudo curl -L https://github.com/docker/compose/releases/download/${VERSION}/docker-compose-$(uname -s)-$(uname -m) -o $DESTINATION
sudo chmod 755 $DESTINATION
```

## Links (depracated)

see [docker website, links](https://docs.docker.com/compose/networking/#links)
Links are a legacy feature of Docker Compose that allow you to connect one service to another (i.e. two containers).
Links allow you to define extra aliases by which a service is reachable from another service. They are not required to enable services to communicate - by default, any service can reach any other service at that service’s name.

<p align="right">(<a href="#top"> back to top </a>)</p>

# Docker engine

## cgrousp

Cgroups are a Linux kernel feature that limits, accounts for, and isolates the resource usage (CPU, memory, disk I/O, network, etc.) of a collection of processes.
A way to limit the resources of a process or a group of processes, and to monitor the usage of those resources:

```bash
# create a cgroup
sudo cgcreate -g memory:mygroup

# set the memory limit
sudo cgset -r memory.limit_in_bytes=100M mygroup

# run a process in the cgroup
sudo cgexec -g memory:mygroup /bin/bash

# check the memory usage
cat /sys/fs/cgroup/memory/mygroup/memory.usage_in_bytes
```

```bash
docker run --cpus=.5 ubuntu
docker run --memory=100m ubuntu
```

<p align="right">(<a href="#top"> back to top </a>)</p>
