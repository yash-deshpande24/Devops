# Docker Q&A

## 1. What is Docker?
Docker is a containerization platform that allows applications to run consistently across different environments by packaging them with their dependencies.

---

## 2. Why do we use Docker?  
Problem due to:
- Mismatch of versions.
- Environmental issues.

There to solve this problem we use docker

- Fast, consistent delivery of your applications.
- Responsive deployment and scaling.
- Running more workloads on the same hardware.

---

## 3. What is Docker Workflow?

<img width="540" height="281" alt="Workflow docker drawio" src="https://github.com/user-attachments/assets/506c801d-a2bd-44db-9078-1ce6cf086b26" />


- In Docker workflow, we write code, create an image using a Dockerfile, run it as a container, and optionally push it to a registry for deployment and scaling.
  
#### $${\color{blue}\textbf {Docker file}}$$
- Text file that contains set of instructions for building docker image.

#### $${\color{blue}\textbf {Container}}$$
- Containers are instances of Docker images that can be started, stopped, and managed independently.
- Container is relatively well isolated from other containers and its host machine.

---

## 4. What is a Container?
A container is a lightweight, runnable instance of a Docker image that packages an application and its dependencies. It is isolated from other containers and the host, but can be connected to networks and storage. When deleted, its non-persistent state is lost. 


---

## 5. What is Docker Architecture?

<img width="1233" height="651" alt="image" src="https://github.com/user-attachments/assets/3c133cb7-a0e8-4cb2-81d6-e514b55780f3" />


Docker follows a client-server model:

- Docker Client (docker): The primary interface for users to interact with Docker. It sends commands (e.g., docker run) to the Docker daemon.

- Docker Daemon (dockerd): Runs in the background, listens for API requests, and manages Docker objects like containers, images, networks, and volumes.

- Docker Registry: A storage system for Docker images. Docker Hub is the default public registry; you can also use private registries.

- Docker Objects: Components such as images, containers, networks, and volumes that Docker manages.

This architecture allows for efficient container management and scalability across different environments.

---

## 6. What is Docker Daemon?
Docker Daemon is the background service that handles container creation, management, and communication with other daemons.
  
---

## 7. What is a Docker Registry?
A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker looks for images on Docker Hub by default. You can even run your own private registry
  
---

## 8. What are Docker Objects?
When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects.
- Images → Read-only templates used to create containers.
- Containers → Running instances of images.
- Volumes → Persistent storage for containers.
- Networks → Enable communication between containers.
  
---

## 9. What is a Docker Image?
- An image is a read-only template with instructions for creating a Docker container.
- An image is based on another image, with some additional customization.

---

## 10. How do you make a Container Public in Docker?
Container ip should map with instance ip to make container public.

---

## 11. What is Container Networking in Docker?
Container networking allows containers to communicate with each other, with the host, and with external networks. It provides isolation and control over how data flows between containers.

---

## 12. What are Network Drivers in Docker?
Docker provides several network drivers to manage container communication:
- bridge: Default driver for standalone containers on a single host. Containers on the same bridge network can communicate with each other.
- host: Removes network isolation between the container and the Docker host, allowing the container to share the host’s network namespace.
- overlay: Creates a distributed network among multiple Docker daemons, enabling containers on different hosts to communicate. Commonly used in Docker Swarm for multi-host networking.
- macvlan: Assigns a MAC address to a container, making it appear as a physical device on the network. Useful for legacy applications requiring direct network access.
- none: Disables all networking for the container, providing complete isolation. Only the loopback interface is available.


---

## 13. What are Storage Mount Options in Docker?
Docker provides volumes for persistent data, bind mounts for sharing host files, and tmpfs mounts for temporary in-memory storage

#### 1. Volumes

* Managed by Docker, stored in Docker's storage directory.
* Persist data beyond container lifecycle.


#### 2. Bind Mounts

* Mounts host file or directory into container.
* Reflects changes immediately.


#### 3. tmpfs Mounts

* Stores files in host memory (temporary).
* Data lost on container stop.


---

## 14. What is Docker Volume?
Volumes are persistent data stores for containers, created and managed by Docker.

When you create a volume, it's stored within a directory on the Docker host.

Volumes are mounted into multiple containers simultaneously.

---

## 15. What is Dockerfile?
A Dockerfile is a text-based document that's used to create a container image. It provides instructions to the image builder on the commands to run, files to copy, startup command, and more

---

## 16. How do Docker client and daemon communicate? Which API is used?
The Docker client communicates with the Docker daemon using a **REST API** over **UNIX sockets** or **network interfaces** (TCP).

---

## 17. What is dockerd?
`dockerd` is the **Docker daemon**. It listens for Docker API requests and manages Docker objects like images, containers, networks, and volumes.

---

## 18. Which language is Docker written in?
Docker is mainly written in the **Go programming language (Golang)**.

---

## 19. Which technology does Docker use to provide isolated workspace containers?
Docker uses **Linux kernel features** like:
- **Namespaces** → for process and resource isolation  
- **Control Groups (cgroups)** → for resource allocation (CPU, memory, etc.)  
- **Union File Systems (UnionFS)** → for image layering  

---

## 20. What is environment in Docker?
In Docker, **environment** refers to **environment variables** set inside a container using the `-e` flag or in Dockerfile with `ENV`.  
They are used to configure applications without modifying code.

---

## 21. What is the difference between Container and VM?
| Feature       | Container                          | Virtual Machine                |
|---------------|------------------------------------|--------------------------------|
| Isolation     | OS-level isolation                 | Hardware-level isolation       |
| Performance   | Lightweight, faster startup        | Heavy, slower startup          |
| Resource use  | Shares host kernel                 | Requires separate OS per VM    |
| Size          | MBs                                | GBs                            |

---

## 22. What are the principles of Docker images?
1. Images are **layered** (each instruction adds a layer).  
2. Images are **immutable**.  
3. Images are **portable** across environments.  
4. Built from **Dockerfile instructions**.  

---

## 23. Command to list image layers
```
docker history <image_name>
```

---

## 24. Name a registry other than Docker Hub
- **Amazon Elastic Container Registry (ECR)**  
- **Google Container Registry (GCR)**  
- **Azure Container Registry (ACR)**  
- **Harbor**  

---

## 25. Difference between Dockerfile and Docker Compose file
| Dockerfile                         | Docker Compose file                  |
|-----------------------------------|---------------------------------------|
| Defines how to build an image     | Defines how to run containers         |
| Contains build instructions       | Contains services, networks, volumes  |
| Single container focus             | Multi-container orchestration         |

---

## 26. What is an image layer?
An **image layer** is a read-only layer created by each instruction in a Dockerfile.  
Layers are stacked to form a complete image.

---

## 27. How is layering possible in an image?
Layering is possible using **Union File Systems (UnionFS)**, which allows multiple read-only layers to stack and appear as a single filesystem.

---

## 28. What is stacking the layers?
**Stacking layers** means combining multiple image layers (read-only + writable) to form a complete container filesystem.

---

## 29. What are Dockerfile instructions?
Some common Dockerfile instructions:  
- `FROM` → base image  
- `RUN` → execute commands  
- `COPY` / `ADD` → add files  
- `CMD` / `ENTRYPOINT` → default command  
- `ENV` → set environment variables  
- `EXPOSE` → define ports  
- `WORKDIR` → set working directory  

---

## 30. What is build cache and how does it work?
The **build cache** stores results of previous Docker builds.  
If an instruction and its context haven’t changed, Docker reuses the cached layer instead of rebuilding it, speeding up builds.

---

## 31. What are Dockerfile stages?
Docker supports **multi-stage builds**:  
- Allows multiple `FROM` statements.  
- Each stage builds an image.  
- Final image copies only necessary artifacts, making it smaller.  

---

## 32. What is host port and container port?
- **Container port** → The port exposed inside the container.  
- **Host port** → The port on the host machine mapped to the container port for external access.  

---

## 33. What is the difference between Registry and Repository?
- **Registry** → A storage and distribution system for Docker images (e.g., Docker Hub, AWS ECR).  
- **Repository** → A collection of related Docker images (different versions/tags) stored in a registry.  

Example:  
- Docker Hub = Registry  
- `nginx` (with tags like `1.19`, `1.20`) = Repository  

---

## 34. What is Docker Compose?
Docker Compose is a tool to **define and manage multi-container applications** using a YAML file (`docker-compose.yml`).  
It allows you to configure services, networks, and volumes, and run them with:  
```
docker-compose up
```

---

## 35. What is a Multi-Stage Build?
A multi-stage build in Docker allows multiple FROM statements in a Dockerfile.

Each FROM starts a new stage.

You can copy only the required artifacts from one stage to another.

Helps reduce final image size by excluding unnecessary dependencies.

---

## 36. What is the difference between Volume and Bind Mounts?

| Feature     | Volumes                       | Bind Mounts                  |
| ----------- | ----------------------------- | ---------------------------- |
| Storage     | Managed by Docker             | Uses exact host path         |
| Portability | Portable across systems       | Tied to host filesystem      |
| Backups     | Easy to back up               | Harder to back up            |
| Use Case    | Best for production workloads | Best for local dev/debugging |

---
## 37. What are the two primary storage options in Docker?
Docker provides two main storage options:

1. **Volumes** → Managed by Docker, stored in Docker's storage area.  
   - Best for production use.  
   - Portable and easy to back up.  

2. **Bind Mounts** → Directly map a host directory/file into the container.  
   - Useful for local development.  
   - Depends on host filesystem path.  

---
## 38. What is Docker Client?
The **Docker Client** is a command-line tool (`docker`) that allows users to interact with the Docker daemon.  
- It sends requests (using Docker REST API) to the daemon (`dockerd`).  
- Commands like `docker run`, `docker build`, `docker ps` are executed via the client.  

---

## 39. What is Docker Networking?
**Docker Networking** allows containers to communicate with each other, the host, and external systems using network drivers.  
- It creates isolated networks for containers.  
- Ensures connectivity and security between services.  

---

## 40. By Default, Container Uses Which Network Driver?
By default, a container uses the **bridge** network driver.  
- Containers in the same bridge network can talk to each other using IP or container name.  

---

## 41. What are Network Drivers in Docker?
**Network drivers** are plugins used by Docker to connect containers to networks.  
- They decide how containers communicate with each other, the host, and the outside world.  

---

## 42. Types of Network Drivers
1. **Bridge** – Default, connects containers on the same host.  
2. **Host** – Shares host’s network namespace (no isolation).  
3. **Overlay** – For multi-host networking (used in Swarm/K8s).  
4. **Macvlan** – Assigns a MAC address, container looks like a physical device.  
5. **None** – Disables networking.  

---

## 43. What is Default Gateway Priority?
The **default gateway priority** decides which gateway (route) a container will use when multiple gateways exist.  
- Lower metric value = higher priority.  

---

## 44. What is Gateway in Network with Highest Priority?
The **gateway with the lowest metric value** is chosen as the highest priority gateway.  
- It becomes the main path for sending traffic outside the network.  

---

## 45. Who Does Dynamic Subnetting and IP Address Allocation for Dockers?
The **Docker daemon (dockerd)** with its built-in **IPAM (IP Address Management)** handles:  
- Assigning subnets.  
- Allocating IP addresses dynamically to containers.  

---

## 46. What is Container DNS Setting?
Docker configures an internal **DNS server** inside containers.  
- It resolves container names to IP addresses.  
- Uses `/etc/resolv.conf` to manage DNS settings.  

---

## 47. What is Custom Host?
A **custom host** in Docker means defining host-to-IP mappings inside a container.  
- Can be set with `--add-host` flag while running a container.  
- Example: `docker run --add-host mydb:172.20.0.10`  

---

## 48. What is Proxy Server?
A **proxy server** acts as an intermediate between a client and server.  
- Forwards requests from client → server.  
- Used for security, caching, and hiding client identity.  

---

## 49. What is DNAT Filter?
**DNAT (Destination Network Address Translation)** filter modifies the **destination IP address/port** of packets.  
- Commonly used in port forwarding (e.g., `80 → 8080`).  

---

## 50. What is NAT and PAT?
- **NAT (Network Address Translation):** Maps private IPs to public IPs for internet communication.  
- **PAT (Port Address Translation):** Extends NAT by also translating port numbers, allowing many devices to share one public IP.  

---


# Doker File

| Instruction | Description |
|-------------|-------------|
| ADD         | Add local or remote files and directories. |
| ARG         | Use build-time variables. |
| CMD         | Specify default commands. |
| COPY        | Copy files and directories. |
| ENTRYPOINT  | Specify default executable. |
| ENV         | Set environment variables. |
| EXPOSE      | Describe which ports your application is listening on. |
| FROM        | Create a new build stage from a base image. |
| HEALTHCHECK | Check a container's health on startup. |
| LABEL       | Add metadata to an image. |
| MAINTAINER  | Specify the author of an image. |
| ONBUILD     | Specify instructions for when the image is used in a build. |
| RUN         | Execute build commands. |
| SHELL       | Set the default shell of an image. |
| STOPSIGNAL  | Specify the system call signal for exiting a container. |
| USER        | Set user and group ID. |
| VOLUME      | Create volume mounts. |
| WORKDIR     | Change working directory. |

---

## Difference between COPY and ADD

| Feature        | COPY | ADD |
|----------------|------|-----|
| Purpose        | Copies files/directories from local system to container. | Copies files/directories and can also fetch from remote URLs or extract compressed files. |
| Functionality  | Simple, predictable, only for local copy. | More powerful (supports remote URLs and auto-extracts `.tar` archives). |
| Best Practice  | Preferred for clarity and consistency. | Use only when extra features (URL or archive extraction) are needed. |

---

## Difference between CMD and ENTRYPOINT

| Feature        | CMD | ENTRYPOINT |
|----------------|-----|------------|
| Purpose        | Provides default command/arguments for a container. | Defines the main executable that always runs. |
| Overriding     | Overridden completely when arguments are passed in `docker run`. | Arguments passed in `docker run` are appended to ENTRYPOINT. |
| Use Case       | Good for default values (e.g., parameters). | Good for fixed commands with flexible arguments. |
| Example        | `CMD ["nginx", "-g", "daemon off;"]` | `ENTRYPOINT ["nginx"]` (then `docker run <image> -g daemon off;`) |

---
## 51. What is exit Codes in docker?
Exit codes are used by container engines, when a container terminates, to report why it was terminated.

| Exit Code | Meaning          | Simple Explanation                                |
| --------- | ---------------- | ------------------------------------------------- |
| **0**     | Success          | Container stopped normally, no error.             |
| **1**     | Error            | Something went wrong inside the container.        |
| **126**   | Not executable   | Command exists but can’t run.                     |
| **127**   | Not found        | Command not found inside the container.           |
| **137**   | Killed           | Force killed (e.g., `docker stop` or low memory). |
| **139**   | Crash (Segfault) |                                                   |

---
