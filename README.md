# Docker Notes

This repo is about Docker Containers. Notes and commands.

### What is a container?
It is an isolated instance of user space

### How does containers work?
- Each container has its own copy of the root filesystem.
- Each container has a process tree.
- Each container of network stack.

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

- Containers are to virtual machines as threads are to processes.

#### LXC - Linux Containers
LXC is a userspace interface for the Linux kernel containment features.


## What is Docker?
Docker is both as company and a container runtime.
Docker leverages (bring together) Linux namespaces, cgroups and capabilities into a product. Docker is a software tool chain for managing LXC containers.
Docker is written in the ___go___ programming language by Google.

- [Resource(http://etherealmind.com/basics-docker-containers-hypervisors-coreos/)]

What is the difference between Docker and Linux LXC?
- Docker used to reply on and depend on LXC versions.
- Docker does not control LXC development.

Docker decided to write an open-source execution driver called ___libcontainer___.
So Docker sees `libcontainer` as the LXC.
Furthermore, `libcontainer` allows Docker to go cross-platform. Thus, `libcontainer` is the default execution driver for Docker.

#### Docker has 3 key components
- Container Engine
- Registry
- Tools

The container will work on any cloud/laptop/VM that has the Docker Engine(runtime)

#### Docker Components Analogy
- Docker Engine (Docker daemon, Docker runtime) -> Shipping yard
- Docker Images -> Shipping container manifest
- Docker Container -> Shipping containers.

## Docker commands
- Start the Docker Engine<br>
`$ service docker start`<br>docker start/running process PID

#### Container Lifecycle
- `$ docker create` creates a container but does not start the container.
- `$ docker run` creates and starts a container in one operation.
- `$ docker start` starts a container so it is running.
- `$ docker restart` stops and starts a container.
- `$ docker pause` pauses a running container, "freezing" it in place.
- `$ docker unpause` will unpause a running container.
- `$ docker attach` will connect to a running container.
- `$ docker stop` stops a running container.
- `$ docker wait` blocks until running container stops.
- `$ docker kill` sends a SIGKILL to a running container.
- `$ docker rm` deletes a container.
- `$ docker update` updates a container's resource limits.
- `$ docker rmi` delete a container image.

#### Container Info
- `$ docker ps` shows running containers.
- `$ docker logs` get logs from container.
- `$ docker inspect` looks at all the info on a container. Outputs a JSON
- `$ docker events` gets events from container.
- `$ docker port` shows running processes in container.
- `$ docker top` shows running processes in container.
- `$ docker stats` shows containers' resource usage statistics.
- `$ docker diff` shows changed files in the container's filesystem.
- `$ docker ps -a` shows running and stopped containers.

#### Import/export
- `$ docker cp` copies files or folders between a container and the local filesystem.
- `$ docker export` turns container filesystem into a tarball archive stream to STDOUT

#### Executing commands
- `$ docker exec` to execute a command in container.
