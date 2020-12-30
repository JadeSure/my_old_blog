---
layout:     post
title:      Docker Operation and debug for Win10 pro(AMD 3600X CPU)
subtitle:   Docker Introduction
date:       2020-12-30
author:     Shuo Wang
header-img: img/post-bg-docker.png
catalog: true
tags:
    - docker image
    - docker container
    - docker repository
---

# What is Docker?
Docker is a tool that allows developers, sys-admins etc. to easily deploy their applications in a sandbox (called containers) to run on the host operating system i.e. Linux. The key benefit of Docker is that it allows users to package an application with all of its dependencies into a standardized unit for software development. Unlike virtual machines, containers do not have high overhead and hence enable more efficient usage of the underlying system and resources.


# What is Container? Different with Virtual Machine?
The industry standard today is to use Virtual Machines (VMs) to run software applications. VMs run applications inside a guest Operating System, which runs on virtual hardware powered by the server’s host OS.

VMs are great at providing full process isolation for applications: there are very few ways a problem in the host operating system can affect the software running in the guest operating system, and vice-versa. But this isolation comes at great cost — the computational overhead spent virtualizing hardware for a guest OS to use is substantial.
Containers take a different approach: by leveraging the low-level mechanics of the host operating system, containers provide most of the isolation of virtual machines at a fraction of the computing power.

Containers offer a logical packaging mechanism in which applications can be abstracted from the environment in which they actually run. This decoupling allows container-based applications to be deployed easily and consistently, regardless of whether the target environment is a private data center, the public cloud, or even a developer’s personal laptop. This gives developers the ability to create predictable environments that are isolated from the rest of the applications and can be run anywhere.
From an operations standpoint, apart from portability containers also give more granular control over resources giving your infrastructure improved efficiency which can result in better utilization of your compute resources.

Due to these benefits, containers (& Docker) have seen widespread adoption. Companies like Google, Facebook, Netflix and Salesforce leverage containers to make large engineering teams more productive and to improve utilization of compute resources. In fact, Google credited containers for eliminating the need for an entire data center.

# What is the structure of Docker?
Docker Image: The basis of a Docker container. Represents a full application.

Docker Container: The standard unit in which the application service resides and executes.

Docker Engine: Creates, ships and runs Docker containers deployable on a physical or virtual, host locally, in a datacenter or cloud service provider.

repo (Docker Hub(Public) or Docker Trusted): Cloud or server based storage and distribution service for your images.

# My understanding
In oriented programming(e.g. Java): 

java class == image

new instances == container

github == Docker Hub (repo)

Docker focuses more on the system level, which can be used to control the environment in the same version(dependencies). Firstly, users can download an image from Docker Hub, then initialize it to an instance that has the same environment as an image. After editing, this container can be reversed to an image that will be passed to other users to share the same editing and environment. It is very convenient in version control and reproduced the results.

# Basic commands operations
Use docker `container <my_command>`

`create` — Create a container from an image.

`start` — Start an existing container.

`run` — Create a new container and start it.

`ls` — List running containers.

`inspect` — See lots of info about a container.

`logs` — Print logs.

`stop` — Gracefully stop running container.

`kill` — Stop main process in container abruptly.

`rm` — Delete a stopped container.

`docker system df` — show docker disk usage (check how many image and container we are using).

e.g. `docker image ls` — list how many images we have on our local machine

`docker image ls ubuntu`  — list all ubuntu related images

`docker run -it <the first three image ID> bash`  — run a container on top of the image (create a new contianer based on the image)

`docker container ls -a`  — -a means that we list the containers no matter it is exited or up

`docker container start <container ID>` — start the container that is in exited situation

`docker export <container ID> -o <file name>.tar` — export the container in which you have created a new folder to local tar file

`docker import <file name>.tar` — import our modified container(other users') to our docker system; after imported the container as a new local image, we can use docker tag command to give it a repositoriy name and tag by `docker tag <container ID> <repository name>:<tag value>`.

`docker exec -it <container ID> bash` — this command will enter the container that is currently running
## ATTENTION：
    `start` will open a new container rather than enter the previous one
    
`docker image rm <container ID>` — remove image from docker (You may need to remove relative container first by `docker container rm <container ID> or shut down container first before remove container by `docker container stop <container ID>`)

[commands operation docs](https://docs.docker.com/engine/reference/commandline/docker/)

# What's Dockerfile
A text document that contains the commands a uers could call on the command line to assemble an image, which can create an automated build that executes several command-line instructions in succession.

docker file begain with:

`FROM <your system>` eg. ubuntu:16.04

`WORKDIR ./`

more commands, such as COPY, ADD, CMD, ENV [official docs](https://docs.docker.com/)
 
