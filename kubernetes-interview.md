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

- `Kubelet` is important component of Kubernetes, that manages containers within pods on a node.
- It registers the node with the API server, watches for pods that have been assigned to its node, and then ensures that the containers in those pods are running and healthy.
- Deployments can help to scale efficiently scale the number of replica pods, enable the rollout of updated code in a controlled manner, or rollback to a previous version of the deployment, if necessary.

- Example:

  ```yml
  apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: # Name of the deployment
    spec:
        replicas: 3
        selector:
            matchLabels:
            app: # Name of the application
        template:
            metadata:
            labels:
                app: # Name of the application
            spec:
            containers:
            - name: # Name of the container
                image: # Image of the container
  ```

### Difference b/w StatefulSet and Deployment in Kubernetes?

<table>
    <tr>
        <th>StatefulSet</th>
        <th>Deployment</th>
    </tr>
    <tr>
        <td>A collection of identical stateful pods are handeled by the resource.</td>
        <td>Resource Controls Identical Pod deployment.</td>
    </tr>
    <tr>
        <td>helpful in managing stateful applications that need persistent storage with dependable network ID</td>
        <td>Enable's to control application state, and ensure the right number of replicas are always up and running.</td>
    </tr>
</table>

### Services in Kubernetes

- Services are the unified way of accessing the workloads on the pods.
- The idea is to group a set of pods endpoints into a single resource.
- Example:

  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: # Name of the service
  spec:
    selector:
      app: # Name of the application
    ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  ```

### How does Kubernetes manage configuration ?

- Kubernetes uses ConfigMaps and Secrets to manage configuration.
- `ConfigMaps` are used to store non-sensitive data in key-value pairs.
- `Secrets` are used to store sensitive data in key-value pairs.
- These resources have different configurtation from the application code, making updates easier.
- Both are defined in YAML files, and applied to cluster using `kubectl`.
- Kubernetes tracks changes in these resources, triggering updates in pods without needing changes to the application code.

### Describe role of Master node in Kubernetes

- The Master Node is the main node in the Kubernetes cluster.
- It is responsible for cluster management and providing the API that is used to configure and manage resources within the Kubernetes Cluster.

### What is the role of kube-proxy in Kubernetes ?

- The netwroking part of kubernetes that enables communication b/w pods and services is called `kube-proxy`.
- It may be installed on any cluster node
- It maintains network rules for service-to-pod mapping, which provides communication to and from Kubernetes Cluster.

### Explain the concept of Ingress in Kubernetes

- Ingress is a Kubernetes API object that is used to expose HTTP & HTTPS routes from outside the Kubernetes Cluster to the services inside the cluster.
- It provides single entry point into a cluster hence making it simpler to manage applications and troubleshoot routing issues.
- The HTTP/HTTPS request that comes to the cluster first goes to the ingress, and than ingress forwards it to the service.

#### Architecture of Ingress

- Kubernetes Ingress acts like a traffic controller for managing the incoming traffic to the Kubernetes Cluster.
- It manages the external access to services within the kubernetes. 

  ![](./imgs/Kubernetes-Ingress-Architecture-(1).webp)
  
- The Kubernetes ingress Controller helps with the following things:

  - Routing: Defines rules in the Routing Table for external HTTP & HTTP traffic to the inside kubernetes cluster services based on the hostname and paths to different services in the cluster.
  - Load Balancing: It helps in distributing the incoming traffic to mutiple services and pods in the cluster.
  - TLS Termination: handles SSL/TLS termination by allowing to encrypt the traffic from outside the cluster to our services.
  - Reverse Proxy: It functions as a reverse proxy, forwarding requests from clients to appropriate services based on the rules defined.

- Example:

  Use `minikube start` to start the cluster.

  Now, Install the ingress controller on minikube using the command `minikube addons enable ingress`.

  This will automatically configure or start Kuberenetes NGINX Implementation of ingress controller.

  Now, we need to create a ingress rule that the controller can evaluate.

  For, this we first check the list of namespaces using the command `kubectl get ns`

  If you don't have it already use the command `minikube dashbaord` to get `kubernetes-dashbaord` namespace.

  We can now check all the components inside the `kubernetes-dashbaord` using the command `kubectl get all -ns kubsernetes-dashbaord`.

  Now, create the ingress rule for the namespace kubernetes-dashboard.

  `ingres.yml`

  ```yaml
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: # Name of the Ingress
      namespace:
    spec:
        rules:
        - host: # Hostname
            http:
            paths:
    ```

    Use the command `kubectl apply -f ingress.yml` to apply the configuration.

    To verify use the command `kubectl get ingress`. Note down the IP ADDRESS shown.

    Now, if you want you can map this IP Address to a certain domain as follows:

    Use the command `sudo vim /etc/hosts`, and than add `[IP_ADDRESS] domain.extension` to it. Now, when you visit this domain, we can see the kubernetes dashboard there.

#### Types of Ingress

- There are mainly 3 types of Ingress, each having it's own merits and demerits.

  - `Physical Ingress`: involves gaining physical access to a system or network bypassing the physical security measures
  - `Network Ingress`: occurs when attackers gain access of a network through vulnerabilites in the infrastructure such as unsecured wifi attacks, open ports or weak passwords.
  - `Software Ingress`: involves exploiting vulnerabilities in software applications or operating system to authourize access to a system or a network .

### What is a Ingress Controller?

- Ingress controller is a component in kubernetes that is responsible for evaluation and processing of ingress routes.
- It acts as a Reverse Proxy and, Load Balancer.
- In order to make this ingress controller work, we need implementation of ingress and that is called Ingress Controller.
- Therefore before configuring ingress to a cluster we need to install.

#### List of Ingrees Controllers

- Nginx Ingress Controller:

  - It is a popular ingress controller that uses Nginx as a reverse proxy.
  - Configures NGINX to route traffic to kubernetes services
  - It is a high performance edge proxy with a small memory footprint.
  - It is a good choice for small to medium-sized deployments.

- Traefik Ingress Controller:

  - It is a modern HTTP reverse proxy and load balancer that makes deploying microservices easy.
  - It is a cloud-native edge router that can route traffic to different services based on the request.
  - It is a good choice for large deployments.

- HAProxy Ingress Controller:

  - It is a high-performance TCP/HTTP load balancer.
  - It utilizes the HAProxy as it's undrelying proxy for handling incoming traffic.
  - Highly Configurable and suitable for complex routing requirements
  - It is a good choice for large deployments.

- Countour:

  - It is built on the Envoy Proxy.
  - Works seamlessly with Kubernetes offering HTTPS/2 and TLS Termination.

### Difference b/w NodePort, Ingress and Load Balancer

<table>
    <tr>
        <th>Ingress</th>
        <th>NodeProt</th>
        <th>Load Balancer</th>
    </tr>
    <tr>
        <td>Ingress is a Kubernetes API object that is used to expose HTTP and HTTPS routes from outside the cluster to services inside the cluster.</td>
        <td>NodePort is a Service that is accessible on a static Port on each Worker Node in the cluster.</td>
        <td>Load Balancer Service type allows the Service to become accessible externally through a Cloud Provider’s Load Balancer functionality.</td>
    </tr>
    <tr>
        <td>Ingress provides a single entry point into a cluster hence making it simpler to manage applications and troubleshoot routing issues</td>
        <td>NodePort Service makes the external traffic accessible on static or fixed port on each worker Node</td>
        <td>LoadBalancer Service is an extension of NodePort Service. Load Balancing is the process of dividing a set of tasks over a set of resources in order to make the process fast and efficient.</td>
    </tr>
    <tr>
        <td>Ingress is configured with the help of rules that define how to route traffic to different services based on hostnames or paths.</td>
        <td>NodePort is configured by specifying the NodePort and the target port for the service.</td>
        <td>LoadBalancer is als configured same as NodePort.</td>
    </tr>
    <tr>
        <td>No specific port range is defined for Ingress.</td>
        <td>NodePort range is between 30000-32767</td>
        <td>LoadBalancer uses standard HTTP and HTTPS ports</td>
    </tr>
</table>

### What is the role of `etcd` in Kubernetes?

- Etcd is the cluster brain that maintains records of all cluster information, which includes the desired state, the current state, resource configurations, and runtime data.
- It is the cluster brain that informs other processes that including the Scheduler about changes in the cluster state and availability of resources.

### What is a Namespace in Kubernetes?

- Namespaces permit Kubernetes clusters to be organized into virtual sub-clusters, which is useful in situations where a cluster is utilized by several teams or projects. 
- Namespaces allow a cluster to be structured in any number of ways, with each namespace providing logical segregation from the others while maintaining the ability to speak across namespaces.

### Explain the use of Labels and Selectors in Kubernetes.

- Labels and Selectors are essential sections in Kubernetes configuration files for deployments and services because of the way they link Kubernetes services to pods.
- Labels are key-value pairs that identify pods distinctly; the deployment assigns these labels and uses them as a starting point for the pod prior to its creation, and the Selector matches these labels.
- Labels and selectors combine to create connections between deployments, pods, and services in Kubernetes.

### What is Persistent Volume in Kubernetes?

- A Persistent Volume (PV) in Kubernetes is an object that allows pods to access storage from a defined device.
- This device is usually described via a Kubernetes StorageClass.
- When a PV is created individually, it is generated and designated to the specified storage device.
- This method wins out over pretreated storage classes because it gives a better understanding of the workflow.
- Example:

  ```shell
    apiVersion: v1
    kind: PersistentVolume
    metadata:
      name: pv0001
    spec:
        capacity:
            storage: 5Gi
        volumeMode: Filesystem
        accessModes:
            - ReadWriteOnce
        persistentVolumeReclaimPolicy: Retain
        hostPath:
            path: /data
        storageClassName: slow
        mountOptions:
            - hard
            - nfsvers=4.1
        nfs:
  ```

### Explain the differences between a DaemonSet and a ReplicaSet

- ReplicaSet

  - On any node, ReplicaSet will make sure that the number of operating pods in the Kubernetes cluster match the number of pods that is planned.
  - Replicaset most suitable for applications like web applications which are stateless.

- DaemonSet

  - Every node will have just the minimum of one pod of the application that we deployed because of DaemonSet.
  - Stateful applications are best fits for it.

### How do we control the resource usage of POD ?

- With the use of limit and request resource usage of a POD can be controlled.

  - Request:

    - The number of resources being requested for a container.
    - If a container exceeds its request for resources, it can be throttled back down to its request.

  - Limit:

    - An upper cap on the resources a single container can use.
    - If it tries to exceed this predefined limit it can be terminated if K8's decides that another container needs these resources.
    - If you are sensitive towards pod restarts, it makes sense to have the sum of all container resource limits equal to or less than the total resource capacity for your cluster.
  
  - Example:

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
    name: demo
    spec:
    containers:
      - name: example1
      image: example/example1
      resources:
        requests:
          memory: "_Mi"
          cpu: "_m"
        limits:
          memory: "_Mi"
          cpu: "_m"
    ```

### What are the various K8's services running on nodes and describe the role of each service?

- Mainly K8 cluster consists of two types of nodes, executor and master.

  - Executor node: (This runs on master node)

    - `kube-proxy`:

      - This service is responsible for the communication of pods within the cluster and to the outside network, which runs on every node.

      - This service is responsible to maintain network protocols when your pod establishes a network communication.

    - `kubelet`:
      - Each node has a running kubelet service that updates the running node accordingly with the configuration(YAML or JSON) file.
      - NOTE: kubelet service is only for containers created by Kubernetes.

  - Master services:

    - `kube-apiserver`: Master API service which acts as an entry point to K8 cluster.
    - `kube-scheduler`: Schedule PODs according to available resources on executor nodes.
    - `kube-controller-manager`:  is a control loop that watches the shared state of the cluster through the apiserver and makes changes attempting to move the current state towards the desired stable state

### Count the number of stopped, running, and pending pods in a namespace

- To count the number of stopped, running, and pending pods in a namespace, you can use the following command:

  ```shell
  > pending= $(kubectl get pods --all-namespaces --field-selector=status.phase=pending --no-headers | wc -l)
  > running= $(kubectl get pods --all-namespaces --field-selector=status.phase=Running --no-headers | wc -l)
  > stopped= $(kubectl get pods --all-namespaces --field-selector=status.phase=Stopped --no-headers | wc -l)
  > echo "Pending: $pending, Running: $running, Stopped: $stopped"
  ```
  
  Here,

  - `--all-namespaces` is used to get the list of pods in all namespaces.
  - `--field-selector=status.phase=<status>` is used to get the list of pods with the specified status.
  - `--no-headers` is used to remove the headers from the output.
  - `wc -l` is used to count the number of lines in the output.
  - `kubectl get pods --all-namespaces --field-selector=status.phase=<status> --no-headers` is used to get the list of pods in the specified namespace with the specified status.