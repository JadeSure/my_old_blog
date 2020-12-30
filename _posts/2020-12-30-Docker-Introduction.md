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
