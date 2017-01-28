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

#### LXC - Linux Containers
LXC is a userspace interface for the Linux kernel containment features.


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

NOTE:

#### Docker Components Analogy
* Docker Engine (Docker daemon, Docker runtime) -> Shipping yard
* Docker Images -> Shipping container manifest
* Docker Container -> Shipping containers.


## Installation

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
