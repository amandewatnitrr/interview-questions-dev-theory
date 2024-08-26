# Kubernetes

### What is Kubernetes?

- Kuberentes is distibuted Open Source Container Orchestration Platform, that helps us in scheduling and executing application containers within and across clusters.

- It has mainly 2 resources:

  - The Master: Cooredinates all activities in the cluster.

    - Scheduling Applications
    - Maintaining Applications' Desired State
    - Scaling Applications
    - Rolling Out Updates

  - Nodes: Instance of an OS that serves as a Worker Machine in a Kubernetes Cluster.

    - `kubelet`: Agent of Managing and Communicating with the Master.
    - Tool(Docker/Container): Tools for running container operations.

### Kuberenetes Architecture

- Kubernetes follows Master-Slave Architecture.
- It is built from scratch as a flexible group of containers that makes it easy to deploy, manage, and scale applications.

  ![](./imgs/Screenshot%202024-08-25%20at%207.20.34 AM.png)

- Works as a engine that runs on a host machine and takes a set of containers and runs them in a cluster.
- Hidden from the underlying hardware of nodes, it provides a platform for automating deployment, scaling, and operations of application containers across clusters of hosts.

### What is a Pod?

- A Pod is the smallest and simplest object that can be deployed on kubernetes.
- Kubernetes packages one or more containers into a single unit called a Pod.
- Pod runs one level higher than the container.
- A Pod always runs on a Node, but they share a few resources which can be shared volumes, Cluster Unique IP, and info abouyt how to run each container.

  ```bash
  # We can create a pod using the following command:
  > kubectl run pod_name --image=image_name:version
  # Provides you all the information about the pod
  > kubectl describe pod pod_name
  # Delete the pod
  > kubectl delete pod pod_name
  ```

- Services are the unified way of accessing the workloads on the pods.
- The Control plane which is the core of Kubernetes is an API server that lets you query, and manipulate the state of an object in Kubernetes.

### What is Horizontal and Vertical Scaling ? When to use them?

#### Horizontal Scaling:

- It is the process of scaling by adding more machines to your pool of resources.
- It is the most common way to scale an application.
- Horizontal scaling is almost always more desirable than vertical scaling because you don’t get caught in a resource deficit.
- Requires a load balancer, which is a middleware component in the standard three-tier client-server architectural model.
- The load balancer is responsible for distributing user requests (load) among the various back-end systems/machines/nodes in the cluster.
- Each of these back-end machines runs a copy of the software and therefore capable of servicing requests. 
- It may also run a “health check” where the load balancer uses the “ping-echo” protocol or exchanges heartbeat messages with all the servers to ensure they are up and running.

- Benefits of Horizontal Scaling:

  - Uptime of other resources ensured during scaling
  - No single point of failure
  - Cost-effective
  - Easier to run fault-tolerance

#### Vertical Scaling:

- It is the process of scaling by adding more power(CPU, RAM, Storage) to an existing machine.

- Benefits of Horizontal Scaling:
  
  - Easy to implement
  - Less Power and Cooling Consumption
  - Reduced Licensing Expenditures

### How does Kubernetes handle container scaling ?

- To automatically scale the workloads, Kubernetes uses the Horizontal Pod Autoscaling(HPA).
- This means more Pods are added in response to increased load.
- Example:

  ```yaml
  apiVersion: autoscaling/v1
  kind: HorizontalPodAutoscaler
  metadata:
    name: # Name of the HPA
    labels:
      app: # Name of the application
  spec:
    scaleTargetRef:
      apiVersion: apps/v1 # API version of the target
      kind: Deployment # Kind of the target
      name: # Name of the target
    minReplicas: 1
    maxReplicas: 10
    targetCPUUtilizationPercentage: 50
  ```

### What is `kubectl` ?

- `Kubelet` is important component of Kubernetes, that manages containers 