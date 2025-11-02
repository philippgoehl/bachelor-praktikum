# Docker

**Installation**: https://docs.docker.com/get-started/get-docker/
**Docs**: https://docs.docker.com
**Docker Hub**: https://hub.docker.com

## What is Docker

Before Docker, developers had to install and configure all the dependencies for their applications on the host machine.
This made it difficult to move applications from one machine to another, and it was hard to ensure that the application would run the same way on different machines.

Docker packages applications and their dependencies into containers so they can run on any machine.
Containers are lightweight, standalone, and executable packages of software that include everything needed to run an application: code, runtime, system tools, system libraries, and settings.

With Docker, developers do not have to install and configure all the dependencies for their applications.
Instead they can just build a Docker image with all the dependencies and run it on any machine that has Docker installed.

Another advantage is to run different versions of the same software on the same machine.
For example, a developer can run a PostgreSQL 9.6 container and a PostgreSQL 10 container on the same machine without any conflicts.

## Why Use Docker

Instead of having to install PostgreSQL, Redis, Node.js, ... on the local machine, developers can just run those services in Docker containers:

```bash
docker run postgres
docker run redis
docker run node
...
```

This can even be automated with `docker-compose` (see [here](./docker-compose.md)).

## Docker vs. Virtual Machines

An Operating System (OS) consists of two main layers:
The OS Kernel, that interacts between hardware components (CPU, memory, disk, network, ...).
And the OS Applications Layer, that contains the applications that run on the OS (e.g. Google Chrome, Microsoft Word, ...).

Docker virtualizes the OS Applications Layer.
Services and applications run in containers that share the same OS Kernel.
This makes containers lightweight (couple of MB) and fast to start (couple of seconds).

Virtual Machines (VMs) virtualize the OS Kernel and the OS Applications Layer.
Each VM has its own OS Kernel and Applications Layer.
This makes VMs slower to start (couple of minutes) and heavier (couple of GB) than containers.

**But**: VMs are compatible with any OS, while containers are only compatible with the OS Kernel they are built on.
**Example**: You have a Windows OS with a Windows OS Kernel. You can't run a Linux based container on a Windows OS Kernel. You need a Linux OS Kernel to run a Linux based container.
**Solution**: Docker came up with Docker Desktop for Windows and Docker Desktop for Mac which provides a Linux OS Kernel to run Linux based containers. These tools run a Linux VM in the background to allow running Linux based containers on Windows and Mac OS.

## Docker Desktop

Docker Desktop includes the following components:

### Docker Engine

This is the "main" part of Docker.
It is a type of long-running program called a daemon process (the `dockerd` command).
The Docker Engine daemon creates and manages Docker objects, such as images, containers, networks, and volumes.

### Docker CLI Client

This is the command line interface that allows users to interact and communicate with the Docker Engine.
Users can use the Docker CLI client to build, run, and manage Docker containers and images.

**Note**: Docker Desktop also comes with a GUI Client that allows users to interact with Docker using a graphical interface - but in general, the CLI is more powerful and flexible.

### Docker Build

This is a tool that automates the process of building Docker images.
Users can create a `Dockerfile` that specifies the steps needed to build an image, and then use the `docker build` command to build the image.

### Docker Compose

This is a tool that allows users to define and run multi-container Docker applications.
Users can create a `docker-compose.yml` file that specifies the services, networks, and volumes needed for an application, and then use the `docker-compose` command to start and manage the application.

## Images and Containers

An image is a read-only template with instructions for creating a Docker container.
It contains the application code, runtime, libraries, environment variables, and configuration files needed to run an application.
Images are used to create containers.
Docker images are versioned - they have a tag that specifies the version of the image (e.g. `postgres:15.0`).
Every image has a `latest` tag that points to the latest version of the image.

A container is a running instance of an image.
Multiple containers can be created from the same image.

## Docker Registry

A Docker Registry is a service that stores Docker images.
Docker Hub is the biggest public registry for Docker images - but Users can also create their own private registry to store and manage their Docker images.
