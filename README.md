# Docker Notes

This repo is about Docker Containers. Notes and commands.

### What is a container?
It is an isolated instance of user space

### How does containers work?
* Each container has its own copy of the root filesystem.
* Each container has a process tree.
* Each container of network stack.

#### How?
Kernel namespaces -> feature of the Linux kernel.
From the point of view of the host, it is one process tree.
But each container has its own kernel namespace that act like a walls.
The walls shield each container from seeing another's container namespace.

#### The PID namespace
Namespaces allow us to partition different various aspect of the OS (pid, tree, networking, file system and mount).

#### Control Groups (cgroups)
Linux kernels have a feature called control groups (cgroups).
It allows to group together resource and apply limits.
We map each container to a cgroup and then we set limits on resources like CPU and memory.

* Containers are to virtual machines as threads are to processes.

* Containers virtualize at the operating system level, Hypervisors virtualize at the hardware level.

* Hypervisors abstract the operating system from hardware, containers abstract the application from the operation system.

* Hypervisors consumes storage space for each instance. Containers use a single storage space plus smaller deltas for each layer and thus are much more efficient.

* Containers can boot and be application-ready in less than 500ms and creates new designs opportunities for rapid scaling. Hypervisors boot according to the OS typically 20 seconds, depending on storage speed.

* Containers have built-in and high value APIs for cloud orchestration. Hypervisors have lower quality APIs that have limited cloud orchestration value.


## What is Docker?
Docker is both as company and a container runtime.
Docker leverages (bring together) Linux namespaces, cgroups and capabilities into a product. Docker is a software tool chain for managing LXC containers.
Docker is written in the ___go___ programming language by Google.

* [Resources](http://etherealmind.com/basics-docker-containers-hypervisors-coreos/)

What is the difference between Docker and Linux LXC?
* Docker used to reply on and depend on LXC versions.
* Docker does not control LXC development.

Docker decided to write an open-source execution driver called ___libcontainer___.
So Docker sees `libcontainer` as the LXC.
Furthermore, `libcontainer` allows Docker to go cross-platform. Thus, `libcontainer` is the default execution driver for Docker.

#### Docker has 3 key components
* Container Engine
* Registry
* Tools

The container will work on any cloud/laptop/VM that has the Docker Engine(runtime)



#### Docker Components Analogy
* Docker Engine (Docker daemon, Docker runtime) -> Shipping yard
* Docker Images -> Shipping container manifest
* Docker Container -> Shipping containers.


## Docker Installation

#### Prerequisites
* Linux. Minimum kernel 3.10.x or newer. Easy install script by Docker
```
curl -sSL https://get.docker.com/ | sh
```
* OSX. Minimum OSX 10.8 "Mountain Lion" or newer.

There are two installations for OS X.
* [`Docker Toolbox`](https://docs.docker.com/toolbox/overview)
* [`Docker for Mac`](https://docks.docker.com/docker-for-mac)

[See comparison](https://docks.docker.com/docker-for-mac/docker-toolbox/).
If using OS X, the recommendation is to use `Docker for mac`

To get started, visit Docker
[`series of tutorials`](https://docs.docker.com/engine/getstarted/)

## Docker commands
* Start the Docker Engine<br>
`$ service docker start`<br>docker start/running process PID

[`Docker Commands`](https://docs.docker.com/engine/reference/commandline/docker/)

#### Container Lifecycle
* [`docker create`](https://docs.docker.com/engine/reference/commandline/create) creates a container but does not start the container.
* [`docker run`](https://docs.docker.com/engine/reference/commandline/run) creates and starts a container in one operation.
* [`docker start`](https://docs.docker.com/engine/reference/commandline/start)  starts a container so it is running.
* [`docker restart`](https://docs.docker.com/engine/reference/commandline/restart) stops and starts a container.
* [`docker pause`](https://docs.docker.com/engine/reference/commandline/pause/) pauses a running container, "freezing" it in place.
* [`docker unpause`](https://docs.docker.com/engine/reference/commandline/unpause/) will un-pause a running container.
* [`docker attach`](https://docs.docker.com/engine/reference/commandline/attach) will connect to a running container.
* [`docker stop`](https://docs.docker.com/engine/reference/commandline/stop) stops a running container.
* [`docker wait`](https://docs.docker.com/engine/reference/commandline/wait) blocks until running container stops.
* [`docker kill`](https://docs.docker.com/engine/reference/commandline/kill) sends a SIGKILL to a running container.
* [`docker rm`](https://docs.docker.com/engine/reference/commandline/rm) deletes a container.
* [`docker update`](https://docs.docker.com/engine/reference/commandline/update/) updates a container's resource limits.
* [`$ docker rmi`](https://docs.docker.com/engine/reference/commandline/rmi/) delete a container image.

#### Container Info
* [`docker ps`](https://docs.docker.com/engine/reference/commandline/ps) shows running containers.
* [`docker logs`](https://docs.docker.com/engine/reference/commandline/logs) get logs from container.
* [`docker inspect`](https://docs.docker.com/engine/reference/commandline/inspect) looks at all the info on a container. Outputs a JSON
* [`docker events`](https://docs.docker.com/engine/reference/commandline/events) gets events from container.
* [`docker port`](https://docs.docker.com/engine/reference/commandline/port) shows running processes in container.
* [`docker top`](https://docs.docker.com/engine/reference/commandline/top) shows running processes in container.
* [`docker stats`](https://docs.docker.com/engine/reference/commandline/stats) shows containers' resource usage statistics.
* [`docker diff`](https://docs.docker.com/engine/reference/commandline/diff) shows changed files in the container's filesystem.
* [`$ docker stats --all`](https://docs.docker.com/engine/reference/commandline/stats) shows a running list of containers.
* [`$ docker ps -a`](https://docs.docker.com/engine/reference/commandline/ps/) shows running and stopped containers.


#### Import/export
* [`$ docker cp`](https://docs.docker.com/engine/reference/commandline/cp/) copies files or folders between a container and the local filesystem.
* [`$ docker export`](https://docs.docker.com/engine/reference/commandline/export/) turns container filesystem into a tarball archive stream to STDOUT

#### Executing commands
* [`$ docker exec`](https://docs.docker.com/engine/reference/commandline/exec/) to execute a command in container.


### Docker Images

#### Lifecycle
* [`docker images`](https://docs.docker.com/engine/reference/commandline/images) shows all docker images.
* [`docker import`](https://docs.docker.com/engine/reference/commandline/import) creates an image from a tarball.
* [`docker build`](https://docs.docker.com/engine/reference/commandline/build) creates image from Dockerfile.
* [`docker commit`](https://docs.docker.com/engine/reference/commandline/commit) creates image from a container, pausing it temporarily if it is running.
* [`docker rmi`](https://docs.docker.com/engine/reference/commandline/rmi) removes an image.
* [`docker load`](https://docs.docker.com/engine/reference/commandline/load) loads an image from a tar archive as STDIN, including images and tags (as of 0.7).
* [`docker save`](https://docs.docker.com/engine/reference/commandline/save) saves an image to a tar archive stream to STDOUT with all parent layers, tags & versions (as of 0.7).

#### Image Info
* [`docker history`](https://docs.docker.com/engine/reference/commandline/history) shows history of image.
* [`docker tag`](https://docs.docker.com/engine/reference/commandline/tag) tags an image to a name (local or registry).

#### Cleaning up

While you can use the `docker rmi` command to remove specific images, there's a tool called [docker-gc](https://github.com/spotify/docker-gc) that will clean up images that are no longer used by any containers in a safe manner.

### Docker Command Examples

Pull a docker image from docker repo.<br>
```docker pull helloworld```

Load an image from a file.<br>
```docker load < img_file.tar.gz```

Tag an image.<br>
```docker tag <image id> helloworld:0.1```

Save an existing image.<br>
```docker save image:tag | gzip > my_image.tar.gz```

Run an instance (container) of a Docker image.<br>
```docker run helloworld```

Import a container as an image from an image.<br>
```cat my_container.tar.gz | docker import - my_image:my_tag```

Export an existing container.<br>
```docker export my_container | gzip > my_container.tar.gz```

___Difference between loading a saved image and importing an exported container as an image?___ <br>
Loading an image using the `load` command creates a new image including its history. Importing a container as an image using the `import` command creates a new image excluding the history which results in a smaller image size compared to loading an image.

List docker images<br>
```$ docker images```<br>
```
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
helloworld             0.1                 e3756cf362b1        35 minutes ago      153.2 MB
renesaenz/helloworld   0.1                 e3756cf362b1        35 minutes ago      153.2 MB
fridge                 latest              29320411ce1f        20 hours ago        128.1 MB
nginx                  latest              abf312888d13        21 hours ago        181.5 MB
ubuntu                 latest              e4415b714b62        12 days ago         128.1 MB
phusion/baseimage      latest              c39664f3d4e5        4 months ago        225.6 MB
hello-world            latest              c54a2cc56cbb        5 months ago        1.848 kB
ubuntu                 15.04               d1b55fd07600        10 months ago       131.3 MB
coreos/apache          latest              5a3024d885c8        2 years ago         294.4 MB```

Create a container with a specific DNS.<br>
```docker run -dns=8.8.4.4 --name=dnstest```

List existing network drivers.<br>
```docker network ls```
