# Docker

## Table of Contents

+ [References](#references)
+ [Introduction](#introduction)
+ [Installation](#installation)
+ [Image commands](#image-commands)
+ [Container commands](#container-commands)
+ [Connecting to containers](#connecting-to-containers)
+ [Docker Compose](#docker-compose)
+ [Volumes](#Volumes)
+ [Ambients and Hot reload](#ambients-and-hot-reload)


## References

- HolaMundo (2022) _**Aprender Docker ahora. Curso completo gratis desde cero**_ [Video](https://www.youtube.com/watch?v=4Dko5W96WHg). YouTube.


## Introduction

**Image**: Package containing our code and its dependencies. Based on Linux. Images are portable (easy to share), making applications development and deployment much easier.

- __Example__: HTML code, NodeJS code, `.env` file (contains all environment variables), etc.

**Container**: Layers and layers of images, starting from the OS (usually Alpine Linux) and ending at our application (Python, SQL...). There images are lightweight (hundreds of MBs) compared to virtual machines (many GBs).

**Repositories**: Containers are stored in repositories (a kind of GitHub for containers) as images. Two types:

- __Private__:
- __Public__: The most popular one is DockerHub (contains NodeJS, Python, MySQL, Postgres, Golang, some Linux distros, etc.).

**Use cases**:

- Keep versions and apps updated
- Quickly onboard new devs
- No dependencies
- No kernel virtualization (lightweight, better performance)
- Choose platform

Examples:

A dev team use different tools (compiler, OS, dependencies...). However, usually not all of them have the same versions or installations of their tools. Furthermore, a new dev can take a long time to install everything as expected. **Containers** automate these installations (usually with a single command), making the process easier, faster, and reliable.

Once devs finish a development, they give the code and instructions for updating dependencies (may include configuration files) to the Ops team so it can deploy the application (like update servers, set up new servers...). This process is prone to errors (missing instructions, communication issues...). Only after deployment we realize if everything was fine or not. If not, we execute a rollback (return to a previous working version). **Containers** can help here: Devs and Ops build an image. The only dependency it requires to be executed is the __Docker runtime__. This process can be automated using Pipelines, which are provided by version control service providers (GitHub, GitLab, BitBucket...).

**Docker** is a way of virtualization:

- Virtual machines (VMs) are generally based on 3 layers: hardware, kernel, and applications. VMs virtualize both applications and kernel.
- Kernel: Communicates hardware to the applications. Different kernels: Windows, Linux, MacOS, etc.
- Three types of virtualization:
  - Para-virtualization: Host (OS) and Guest (OS of the virtual machine installed on the host). Maximum access to the hardware.
  - Partial virtualization: Some hardware components are virtualized.
  - Complete virtualization: All hardware components are virtualized.
- Docker is superior to any virtualization type since it only virtualizes the applications, and just use the kernel of the OS where it's being executed. Thus, Docker images more lightweight and have better performance.


## Installation

**Docker Desktop** (DD) ([download](https://www.docker.com/products/docker-desktop/)): Optimized virtual machine that runs Linux and executes containers. Allows access to the file system and the network (internal and external). It includes different tools (CLI, Docker Compose...). It can run natively on Windows using the WSL2 (Windows Subsystem for Linux).

**Docker Hub** (DH) ([link](https://hub.docker.com/)): It provides thousands of images for Docker (Ubuntu, mysql, Python, postgres...). Download an image with `docker pull imageName`, specifying the version of the image (if there're many versions).

Install DD. It can be executed with a GUI or the CLI. If using CLI, ensure DD is running in the background.


## Image commands

- `docker images`: Get list of all downloaded images. It specifies the repo name, tag (version), image id (unique image id), creation date, and size.
- `docker pull mysql`: Download from DH the latest version of an image (like `mysql`), or specify a version (like `mysql:9.5.0`). This downloads all necessary layers, except those that you already have.
  - `docker pull --platform linux/x86_64 mongo`: Specifies the platform (`linux/x86_64`) you want to download for `mongo`.
- `docker image rm mysql:9.5.0`: Remove an image (`mysql:9.5.0`).


## Container commands

Every image has configuration variables that we can edit and are used for creating the container.

Some containers need access to some ports, but container ports doesn't work unless you map one port from your physical computer to a container port.

There are a few ways to refer to a `<container>`:

- Id (like `bedeedfd10cab297dc18594e273612f46b6fdb65af26b81eddcd8fb5a8a0dcaf`)
- Abreviated id (like `bedeedfd10ca`)
- Name (like `stoic_stonebraker`)

Some command options: `-p` (port), `-d` (detach), `-e` (environment variable).

- `docker create mysql` (alternative: `docker container create mysql`): Create a container using an image (like `mysql`) as base. This command returns the container ID.
  - `docker create --name <name> mysql`: Create a container and define its name.
  - `docker create -p27017:27017 --name <name> mysql`: Create container, name it, and map a computer port to a container port (-p<computerPort>:<containerPort>`). If we don't specify the container port, Docker will choose one. 
- `docker start <container>`: Run a container.
- `docker ps`: Check running containers.
  - `docker ps -a`: Check all containers (those running and not running).
- `docker logs <container>`: Show logs of a container.
  - `docker logs --follow <container>`: Show logs and keep listening for more. Stop listening with `Ctrl C`.
- `docker stop <container>`: Stop a running container.
- `docker rm <container>`: Remove a container.
- `docker run -d mysql`: Get `mysql` image, create a container, and run it. If the image is not found, it downloads it.
  - We can use here the options used with `docker create` (example: `docker run --name ABC -P27017:27017 -d mysql`).
  - Option `-d` (dettached) makes the container run in a different thread. Not including `-d` will make the CLI show logs in `--follow` mode, and `Ctrl C` will stop the container execution, not just listening to logs.


## Connecting to containers

**Container configuration**: This is done using environment variables (`-e`) during container creation, and a `Dockerfile` file.

**Application communicates with container**: Suppose that we want a container with `mongo` (database system) and we have an application outside that wants to communicate with the database in the container. To be able to access the DB, we need to create the container using some configuration parameters (so the container has a name and password which can be used by the application to access the DB). In DockerHub, `mongo` provides information on how to configure its containers. All containers are configured differently. In this case, we configure the container with:

- `docker create -p27017:27017 --name monguito -e MONGO_INITDB_ROOT_USERNAME=john -e MONGO_INITDB_ROOT_PASSWORD=myPass mongo`

**Container communicates with container**: If we want our application to run inside a container we need to create a file called `Dockerfile`. This file contains the configuration of your container, the instructions it needs to be created. Example file:

```
FROM node:18
RUN mkdir -p /home/app
COPY . /home/app
EXPOSE 3000
CMD ["node", "/home/app/index.js"]
```

1. Any image we create has to be based on another image.
2. Create folder in the container.
3. Copy my source code file from the host to the container.
4. Expose a port to allow others to connect to this container (we, from host, or other containers).
5. Specify the command (and its arguments) that the container has to run to execute our application.

To allow different containers to communicate with each other we need to group them in an "internal network".

- `docker network ls`: List all Docker networks.
- `docker network create mynetwork`: Create network.
- `docker network rm mynetwork`: Delete network.
- `docker build -t myapp:1.0.0. path/to/dockerfile`: Create a Docker image. Parameters: image name (`myapp`), tag (`1.0.0.`), and `Dockerfile`.
- `docker create -p3000:3000 --name chanchito --network mynetwork myapp:1.0.0.`: Create a container (`mongo`) within a network (`mynetwork`). Example for `mongo`:
  - `docker create -p27017:27017 --name monguito --network mynetwork -e MONGO_INITDB_ROOT_USERNAME=nico -e MONGO_INITDB_ROOT_PASSWORD=password mongo`

Containers inside the same internal network communicate with each other using the container's name (the domain name of a container is it's own name). Example: instead of `localhost:27017` we use `monguito:27017`.


## Docker Compose

Docker Compose is a program that simplifies and automates container creation. It's already included in Docker Desktop. It requires you to create a `docker-compose.yml` file and edit it like this:

```
# Example of a comment
version: "3.9"
services:
	chanchito:
		build: .
		ports:
			- "3000:3000"
		links:
			- monguito
	monguito:
		image: mongo
		ports:
			- "27017:27017"
		environment:
			- MONGO_INITDB_ROOT_USERNAME=john
			- MONGO_INITDB_ROOT_PASSWORD=mypass
		volumes:
			- mongo-data:/data/db
			
volumes:
	mongo-data:
```

- `#`: Symbols used for comments.
- `version "3.9"`: Yaml version (`yml`). Yaml is a language for configurations.
- `services`: Containers we want to use (`chanchito`, `monguito`...).
- `build`: Path to the image we want to use to create a container.
- `ports`: List of mapped ports (`3000:3000` = host_port:container_port).
- `links`: Name of containers that will use this container.
- `image`: Image used for building the container.
- `environment`: Environment variables used for building the container.
- Volumes data (see [Volumes](#volumes) chapter):
  - 1st `volumes`: Specify volumes that container `monguito` will use, and their paths within the container where they will be mounted.
	- Note: By default, mongodb stores data in `/data/db`, mysql in `/var/lib/mysql`, and postgres in `/var/lib/postgresql/data`.
  - 2nd `volumes`: Specify names of all volumes used in container in the `docker-compose.yml` file.

Commands:

- `docker compose up`: Use the docker-compose file to build the containers. This creates an image (`mongoapp_chanchito`), two containers (`mongoapp_chanchito`, `mongo`), and an internal network (`mongoapp_default`) containing all containers in the file. Executing this command again will use the previously created containers.
- `Ctrl C`: Stop docker-compose execution (i.e., stop services and unmount containers).
- `docker compose down`: Delete what docker compose created (image, containers, and network).


## Volumes

Volumes is a tool that provides data persistence (useful for development and databases). It allows certain files (folders) in a container to be in the host (mapped from the host), so their content is not deleted each time you delete a container.

Volumes types:

- __Anonimous__ (`- /path/to/mount/in/the/volume:destination/path/in/container`): You only specify the path. Docker decides where to store the volume. This volume cannot be referenced (for example, to allow another container to use it).
- __Host__ (`- mongo-data:/data/db`): You decide which folder to mount and where to mount it.
- __Named__: Similar to Anonimous, but you can reference it when creating another volume, so you can reuse it with the same and other images.

To use volumes, specify the appropriate lines in `docker-compose.yml` as shown in chapter [Docker Compose](#docker-compose).


## Ambients and Hot reload

We might want to configure different development environments: production and development. We can do it by creating a new `Dockerfile` and a new `docker-compose.yml` files for each environment (we might want to use the previous files for production and these new ones for development). Furthermore, we can activate `hot reload` to speed up applications development when using Docker.

`Dockerfile.dev` (its content is based on the previous `Dockerfile`, but adapted to development):

```
FROM node:18

RUN np i -g nodemon
RUN mkdir -p /home/app

WORKDIR /home/app

EXPOSE 3000

CMD ["nodemon", "index.js"]
```

- `nodemon`: Executing an application with `node` won't detect the changes you are doing. This tool recognizes the changes.
- `WORKDIR`: Specify the path where we will be working.

`docker-compose-dev.yml`:

```
version: "3.9"
services:
	chanchito:
		build:
			context: .
			dockerfile: Dockerfile.dev
		ports:
			- "3000:3000"
		links:
			- monguito
		volumes:
			- .:/home/app
	monguito:
		...
```

- `context`: Specify the file where is the application (context) it will be working with.
- `dockerfile`: Specify the `Dockerfile` to use.

Commands:

- `docker compose -f docker-compose-dev.yml up`: Use our custom docker-compose file to build the containers. The `-f` option is used to specify a custom file different than `docker-compose.yml`.

A new developer can start developing in a given environment very quickly only with command `docker compose up`, which downloads dependencies and executes the application.