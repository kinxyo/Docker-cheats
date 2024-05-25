# Docker-cheats

## Responsibilities

1. Facilitate Collobration
2. Automate as much as possible
3. Build infrastructure & mangement it
4. Regularly monitor benchmarks.
5. Data management
7. Assure Quality
6. Security

## Docker

### Why

> [!note]
> We move from one way of doing thing to another because of inconvenience. This is evolution.

A computer is essentially 3 components-- CPU, RAM & Disk.
We cannot utilize this baremetal directly, so we need an abstraction layer for this.

Operating System provides 'Kernel' that acts as the abstraction layer for CPU, RAM & Disk. Operating System manages resource allocations for them.

Hence, an application runs inside Operating System because through kernel it can access computing & storage resources, and Operating System can ensure appropriate amount of resource allocation for an application.

To run an application isolated from local enviornment, it's run in a dedicated server.

Traditionally, 1 server could only handle 1 Operating system, therefore it could deploy only 1 application.

Vmware came out with Virtual Machine, with which, 1 server could now handle multiple Operating System, therefore it can deploy multiple applications.

> Q. **Operating System manages resource allocation and there is only 1 server, so do these multiple Operating System communicate with each other for allocating resource properly?**

No.

- The physical resources of 1 server are divided virtually for each Operating System.
- This is managed by *HyperVisor*.
- Operating System can only allocate the resource to application which are allocated to it via hypervisor.

However, the limited amount of physical resource a server has, had to be divided amongst multiple Operating System, which was still very problematic for applications to run at scale.

Containers came into the picture which enabled running multiple applications isolated-ly in the same Operating System.

### Introduction

**Docker**: a company that made linux containers mainstream.

- `Dockerfile` is template for building docker application, *like a recipe for a dish*.

- *Docker image is like a pre-built binary*. When you will run it, it will run the application. Therefore, you can say that Docker application is running instance of Docker image

- Docker application runs inside container, so whenever *a container is running*; it means *some application is running* via Docker.

So in hindsight,

$running image = container = app$

not literally, but loosely.

### Basic Commands

#### Download an image

```bash
docker pull <image_name>
```

downloads the image from DockerHub.

> **Additional**
> You can specify version for your image via *tag*.
> `docker run <image_name>:<tag>`

#### Run an image

```bash
docker run <image_name>
```

> [!NOTE]
> If the image is not present locally then it will be pulled from dockerhub.

#### See all running images

```bash
docker ps
```

> [!IMPORANT]
> We get to see `container id` of all running images from this command which will come handy in running *container-specific* commands.

#### See all downloaded images

```bash
docker ps -a
```

#### Stop a running container (PAUSE APPLICATION)

```bash
docker stop <container_id>
```

#### Remove a container (END APPLICATION)

```bash
docker rm <container_id>
```

#### Delete all the stopped containers

```bash
docker container prune -f
```

#### Remove an image

```bash
docker rmi <image_name> -f
```

### Advance Commands

#### Run application commands

```bash
docker run <image_name> <application_command>
```

> **Example:**
> ```bash
> $ docker run ubuntu echo heyy
> heyy

#### Run an image in interactive mode

```bash
docker run -it <image_name>
```

#### Run an image in background

```bash
docker run -d <image_name>
```

#### Clean unused Docker objects

- stopped containers
- dangling images
- unused networks

```bash
docker system prune
```

#### Clean unused Docker objects (AGGRESSIVELY)

- also removes unused volumes

```bash
docker system prune -a
```

#### Log

`docker log` provides data that I don't understand.

```bash
docker log --since <timestamp>
```

---
> [!IMPORTANT]
> Run this before starting docker (for ubuntu 24 lts):
> `sudo sysctl -w kernel.apparmor_restrict_unprivileged_userns=0`
