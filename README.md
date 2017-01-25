# Docker Notes

This repo is about Docker Containers. Examples and commands.

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

## What is Docker?
Docker is both as company and a container runtime.
Docker leverages (bring together) Linux namespaces, cgroups and capabilities into a product. Thus, Docker provides a uniform runtime environment.
Docker is written in the ___go___ programming language by Google.

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
