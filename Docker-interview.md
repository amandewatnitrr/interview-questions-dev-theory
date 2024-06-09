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