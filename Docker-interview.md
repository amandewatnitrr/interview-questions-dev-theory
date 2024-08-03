# Docker Interview Questions

### Explain the Internal Working of Docker

- Docker uses the `Union File System` to create and layer Docker Images.
- The images are built on top of base images, actions are than added to that base image. And, this creates a new image.
- It allows files and directories of seprate file system known as branches, form a single file system.
- When building a image docker will save these branches in it's cache, it will re-use the branch, not the command, which is a cache-hit. This known as `Docker Layer Caching`.<br/>
- The Docker Engine combines the namespace, cgroups and UFS into a format called `Container Format`. The default container format is `libcontainer`.

- ![](./imgs/Screenshot%202024-06-09%20at%203.13.48 PM.png)

- `Union File Systems`

  - Uniong File Systems oprate by creating layers, making them light-weight and fast.
  - Docker uses UFS to provide building blocks for containers.

- `cgroups & namespaces`
  
  - `cgroups` or Control Groups and Kernel Namespaces are the backbone of Docker. With `cgroups`, provided by linux resource management and allocation for processes become easy.
  - Namespaces are helpful in isolating the processes, so that they can't interfere with each other.
  - By default, there are 6 namespaces in Docker:

    - `PID` - Process Isolation
    - `NET` - Network Isolation
    - `IPC` - Inter Process Communication
    - `MNT` - Mount Point Isolation
    - `UTS` - Hostname and Domain Isolation
    - `USER` - User Isolation

  - Each container has it's own namespace and processes, and will not have access to anything outside it's namespace.

- `libcontainer/runC`

  - `libcontainer`, a C Library provides docker it's underlying functionality.
  - Each container has it's own root file system, and the underlying host doesnot let the process leave the directory also called `chroot jail`.

### Drawbacks of Docker

- Docker engine requires root previlages to run the containers.

### How many docker components are there??

- There are mainly 3 docker components:
  - Docker Client
  - DOcker Host
  - Docker Registry
  
- Docker Client: performs `build` and `run` operations for opening comminication with the Docker host.
- Docker Host: It has the docker daemon, which is responsible for creating, running and managing the containers, opens connection to the docker registry.
- Docker Registry: It stores the Docker images. This registry can be a public or a private registry.
  
![](./imgs/Screenshot%202024-07-14%20at%204.15.49 PM.png)

### What is Virutalization??

- Virtualization

  - Virtualization is creating software-based replica of physical machine, allowing you to run multiple isolated multiple environments on same hardware across distributed systsm.
  - The System hare a common server with a hypervison on top of the Host OS, on which the Application runs.
  - Each VM has it's own OS, and the hypervisor allocates the resources to the VMs.
  - Each VM requires it's own set of resources.
  - Lesss portable due to varying Guest OS.
  - Slower Deployment times due to OS Boot Process

- Containerization
  
  - Containerization is a lightweight form of virtualization, where the containers share the host OS kernel and makes use of the host OS system libraries.
  - Containers provide isolation b/w these applications making sure they don't interfere with each other.
  - The Continers encapsulates the dependencies and configurations, making it easy to share and run the application on different environments.
  - Containers are light-weight compared to VMs, as they share the Host OS Kernel.
  - The containers share the host resources.
  - Highly portable across different systems.

### What is a `Docker Image` ??

- A Docker Image is a file, comprised of multiple layers, containing the code, dependencies, and packages associated with the software for creating the containers.

### RUN vs CMD vs ENTRYPOINT

- `RUN` - Executes command in a new layer and creates a new image.Commonly used for installing packages.
  - Shell form: `RUN <command>`
  - Exec form: `RUN ["executable", "param1", "param2"]`
  - Example: `RUN apt-get install python3`

- `CMD` - Sets default command and parameters.
  - Can be overridden from command line when docker container runs.
  - Shell form: `CMD <command>`
  - Exec form: `CMD ["executable", "param1", "param2"]`
  - Example: `CMD ["python3", "app.py"]`

- `ENTRYPOINT` - Allows you to configure a container that will run as an executable.
  - Entrypoint arguments are always used, and are appended to the end of the command.
  - Shell form: `ENTRYPOINT <command>`
  - Exec form: `ENTRYPOINT ["executable", "param1", "param2"]`
  - Example: `ENTRYPOINT ["python3", "app.py"]`

### What is the function of a `Hypervisor`??

- Hypervisor is a software that makes virtualization possible. It is also reffered as Virtual Machine Monitor (VMM).
- It divides the resources among the host system and, allocates them to each guest environment installed.
- This means multiple OS can be installed on a single host system.
- Hypervisor are of 2 types:

  - Native Hypervisor:
    - Also known as Bare Metal Hypervisor.
    - Runs directly on the underlying host system
    - Ensures direct access to host hardware, which is why it doesn't require a base OS.

  - Hosted Hypervisor:
    - Makes use of underlying Host Operating System which has the existing OS Installed.

### What is `Docker Namespace` ??

- `namespace` is a feature of the Linux kernel that isolates and separates system resources.
- It is a core concept behind containerization, as it introduces a layer of isolation among containers.
- It makes sure that the containers are portable, and donot affect the underlying host.

### How to save and load Docker Images??

- `docker save` - Saves one or more images to a tar archive.
  - `docker save -o <path to save> <image name>`
  - Example: `docker save -o /tmp/my_image.tar my_image`
  
- `docker load` - Loads an image from a tar archive.
  - `docker load -i <path to tar file>`
  - Example: `docker load -i /tmp/my_image.tar`

### Can you tell the what are the purposes of `up`, `run`, and `start` commands of `docker compose`?

- `docker-compose up`
  - Builds, (re)creates, starts, and attaches to containers for a service.
  - By default it runs in the attached mode, which means it will show the logs of all the containers.
  
  - If we run it in `attached` mode, it will show the logs of all the containers.
    - Example: `docker-compose up`

  - If we run it in `detached` mode, it will run the containers in the background.
    - Example: `docker-compose up -d`
  
- `docker-compose run`
  - Runs a one-time command against a service.
  - Here, the service name needs to be specified, and the docker will start that, including the one the target service is dependent on.
  - Mainly, used for running tests, or debugging.
  - Expample: `docker-compose run <service-name> <command>`
    - `docker-compose run web python manage.py test`

- `docker compose start`
  - Starts existing containers for a service.
  - It will start the containers which are stopped.
  - Not useful for creating new containers.
  - Example: `docker-compose start

### Can you differentiate b/w `Container Logging` and `Daemon Logging`??

- `Container Logging`
  - Logs generated by the containers.
  - These logs are stored in the container itself.
  - These logs can be accessed using the `docker logs` command.
  - Example: `docker logs <container-name>`
  - Can be done using command `sudo docker run -it <container-name> /bin/bash`.

- `Daemon Logging`
  - This kind of logging has 4 levels of logging:
    - `Debug`
    - `Info`
    - `Error`
    - `Fatal`

  - `Debug` has all the data about what happened during the execution of daemon process.
  - `Info` has all the information including the error information during the execution of daemon process.
  - `Errors` have the errors that happended during the daemon process.
  - `Fatal` has the fatal errors that occured during the execution.

### Difference b/w `Docker Image` and `Layer`.

- A `Docker image` is a series or collection of layers of instructions containing dependencies, packages, and code required to create a executable software bundled together.
- A `Layer` is a instruction corresponding to the instruction on the Dockerfile. Each instruction in the Dockerfile creates a layer in the image.

### Difference b/w `COPY` and `ADD` in Docker.

- Both `COPY` and `ADD` have same functionality, but `COPY` is preferred over `ADD` because it is more transparent.
- `COPY` is used to copy files and directories from the host to the container.
- `ADD` is used to copy files and directories from the host to the container, but it also supports URLs and extracting tar files.

### Can a Container restart itself??

- Yes, a container can restart itself. We can use the `--restart` flag with the `docker run` command to restart the container.
- But, there are some policies that can be used with the `--restart` flag:
  - `no` - Never restart the container.
  - `always` - Always restart the container.
  - `on-failure` - Restart the container if it exits with a non-zero status.
  - `unless-stopped` - Always restart the container unless it is explicitly stopped.
- The policies can be used as: `docker run --restart=<policy-value> <image-name>`.

### Can we use JSON instead of YAML for Docker Compose??

- Yes, we can use JSON instead of YAML for Docker Compose. We can use the `--file` or `-f` flag with the `docker-compose` command to specify the JSON file.
- Example: `docker-compose -f docker-compose.json up`.

### Describe the lifecycle of a Docker Container.

- The Different stages a container goes through from the creation of the container to it's end is called Docker Container Lifecycle.
  - Created: The container has just been created with a new name, but has not yet been started.
  - Running: In this state, the container is running with all it's associated process.
  - Paused: State happens when a running container is paused.
  - Stopped: State happens when the running container is stopped.
  - Deleted: Container is in dead state.

### How do you get the number of containers running and paused??

- We can do so using the following command:
  - Running: `docker ps -q | wc -l`
  - Paused: `docker ps -aq -f "status=paused" | wc -l`
  - Stopped: `docker ps -aq -f "status=exited" | wc -l`

- Now, let's break down the command:
  - `-a`: Gives all the containers
  - `-q`: Gives only Numeric ID of the container
  - `-f "status=<status>"`: flag filters and gives only the containers with specified status
  - `|`: This is a pipe. It takes the output from the command on the left and, feeds it as input to the command on the right of the pipe.
  - `wc -l`: `wc` here is word count. And, `-l` flag specifies to count the number of lines in the output.


### What does `docker sytsem prune` command do??

- The `docker system prune` command cleans docker by removing the unused data. This includes:
  - Stopped Contianers
  - Unused Networks
  - Dangling Images(Images not associated with any container)

### How do you scale docker containers horizontally??

- Horizontal Scaling of Docker Container can be achieved by replicating the service through multiple nodes.
- We can do so using docker compose using the command: `docker-compose up --scale <service-name>=<number-of-instances>`.
- We can do the same using docker-swarm using the command: `docker service scale <service-name>=<number-of-instances>`.

### What is `Docker Swarm`??

- `Docker Swarm` is a clustering and orchestrating tool that runs on Docker Application.
- It helps end-users to create and manage a cluster of Docker nodes as a single virtual system.
  

### How will you ensure `Container-1` runs before `Container-2` using docker-compose??

- For this purpose we use the `depends_on` attribute with `docker-compose.yaml` file.
- Example:

  ```yaml
  version: 3
  services:
    backend:
      build: .
      depends_on:
        - db

    db:
      image: postgres # Postgres will be the 1st Container to come up, and than the backend container will come up.
  ```


### Write a sample Dockerfile for a Python Application exposing on port 3000

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.9

# Set the working directory to /app
WORKDIR /app
COPY . /app
RUN pip install --no-cache-dir -r requirements.txt
RUN ["python3", "app.py"]

# Make port 3000 available to the world outside this container
EXPOSE 3000
```

### What is Docker Compose?

- Docker Compose is a tool for defining and running multi-container Docker applications.
- With Compose, you use a `YAML` file to configure your application's services.
- Then, with a single command, you create and start all the services from your configuration.
- Example of `docker-compose.yml` file:

```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
    depends_on:
      - redis
  redis:
    image: "redis:alpine"
```

### Let's say we have multiple containers running on a single host, how can we access the container from the host?

- We can access the container from the host using the `docker exec` command.
- Example: `docker exec -it <container-name> /bin/bash`

### How will we monitor a docker in production?

- We can monitor a docker in production using the following tools:
  - `Prometheus`
  - `Grafana`
  - `ELK Stack`
  - `Datadog`
  - `Sysdig`
  - `Docker Stats`
  - `cAdvisor`
  

### What is load balancing?? How can we achieve load balancing in Docker?

- Load Balancing is the process of distributing incoming network traffic across multiple servers.
- We can achieve load balancing in Docker using the following ways:
  - `Docker Swarm`
  - `NGINX`
  - `HAProxy`
  - `Traefik`
  - `Consul`
  - `Fabio`

- We can also use `Docker Compose` to achieve load balancing. We can use the `scale` command to scale the services.
  - Example: `docker-compose up --scale <service-name>=<number-of-instances>`.

- It plays a crucial role in ensuring high availability and reliability of the application.

### How do you perform live migration of Docker Containers b/w hosts??

- We can perform live migration of Docker Containers between hosts using the following ways:
  - `docker checkpoint`
  - `docker swarm`
  
  - Example:

      ```bash
      docker run -d --name my-container my-image # Run the container
      docker checkpoint create my-container checkpoint1 # Create a checkpoint
      scp -r /var/lib/docker/containers/<container-id>/checkpoints/checkpoint1 user@remote-host:/var/lib/docker/containers/<container-id>/checkpoints/ # Copy the checkpoint to remote host
      ssh user@remote-host # SSH into the remote host
      docker start --checkpoint checkpoint1 my-container  # Start the container on the remote host
      ```

- Using `docker swarm` we can perform live migration of containers between hosts.

### How do you share data b/w containers in Docker?

- We can share data between containers in Docker using `-v` flag. This flag is used to create a volume in the container.
- Example:

  ```bash
  docker run -d --name container1 -v /data alpine # Create a volume in container1
  docker run -d --name container2 --volumes-from container1 alpine # Create a volume in container2 and share data from container1
  ```

### How Do You Debug Issues in a Docker Container?

- We can debug issues in a Docker Container using the following ways:
  - Container Logs: `docker logs <cid/>` helps in viewing the output and the error logs of the container.
  - Interactive Shell: `docker exec -it <cid/> /bin/bash` helps in accessing the interactive shell inside the container.
  - `docker attach`
  - Inspect Container Details: `docker inspect <cid/>` helps in retreiving the detailed information about the container.
  - `docker events`
  - `docker top`
  - `docker diff`
  - `docker cp`
  - `docker port`
  - `docker stats`
  - `docker system df`
  - `docker system events`