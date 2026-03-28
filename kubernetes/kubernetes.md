# Kubernetes Components

![kube-components](images/kube-components.jpg)

ETCD -> etcd is an open-source, distributed key-value storage system that facilitates the configuration of resources, the discovery of services, and the coordination of distributed systems such as clusters and containers. Its functionalities include distributing and scheduling work across multiple hosts, enabling automatic updates that are safer, and setting up overlay networking for containers. etcd is designed to maintain redundancy and resilience in cloud systems and is the standard storage system used in Kubernetes. 

api server -> The API server in Kubernetes is the core control plane component that provides an interface to the Kubernetes API. It accepts, processes, and validates requests from users, applications, and other Kubernetes components, maintaining state consistency across the cluster. Think of it as the “traffic controller” for your cluster—directing requests, enforcing rules, and ensuring everyone follows the plan.

Scheduler -> The Kubernetes scheduler is a control plane process which assigns Pods to Nodes. The scheduler determines which Nodes are valid placements for each Pod in the scheduling queue according to constraints and available resources. The scheduler then ranks each valid Node and binds the Pod to a suitable Node. Multiple different schedulers may be used within a cluster; kube-scheduler is the reference implementation. See scheduling for more information about scheduling and the kube-scheduler component.

Controller -> In robotics and automation, a control loop is a non-terminating loop that regulates the state of a system.

Here is one example of a control loop: a thermostat in a room.

When you set the temperature, that's telling the thermostat about your desired state. The actual room temperature is the current state. The thermostat acts to bring the current state closer to the desired state, by turning equipment on or off.

In Kubernetes, controllers are control loops that watch the state of your cluster, then make or request changes where needed. Each controller tries to move the current cluster state closer to the desired state.


Container runtime -> A container runtime is the foundational software that allows containers to operate within a host system. Container runtime is responsible for everything from pulling container images from a container registry and managing their life cycle to running the containers on your system.

Kubelet -> A Kubelet in Kubernetes is a crucial component of the primary node agent that runs on each node. It assists with container management and orchestration within a Kubernetes cluster. Kubelet supports communication between the Kubernetes control plane and individual nodes and it also enables the efficient deployment and execution of containerized applications across the cluster.

## Master vs Worker Nodes

![master-vs-worker-nodes](images/master-vs-worker-nodes.png)


## Cluster Info

Run on cluster:
```bash
kubectl run hello-minikube
``` 

Info about cluster:
```bash
kubectl cluster-info
``` 

List nodes of the cluster:
```bash
kubectl get nodes
``` 

# CRI

Container runtime interface allowes any solution to act as cointainer runtime as long as they implement OCI standart.

### OCI standart
  - image spec - specification on how an image should be built
  - runtime spec - how any container runtime should be developed


Containerd - docker pulled its core container runtime into a standalone project. Containerd is CRI compatible so it can be used separately. 

### ctr 
  - comes with containerd
  - not very user friendly
  - limited feature support 

### nerdctl:
  - provides a Docker like CLI for containerd
  - nerdctl suppports Docker compose
  - nerdctl supports newest features
  - supports encrypted container images
  - lazy pulling
  - P2P image distribution
  - Image signing and verifying

```bash
nerdctl run --name redis redis:alpine
nerdctl run --name webapp -p 80:80
``` 

### crictl 
 - from kubernetes prospective tool which works with all compatible runtimes
 - installed separately
 - used to inspect and debug container runtimes
 - not to create containers
 - works across different runtimes
 - if you create container on kubernetes kubelet will delete container

```bash
crictl pull busybox
crictl images
crictl ps -a
crictl logs <name>
crictl pods
``` 

### Extract pod definition from run

```bash
kubectl run redis --image=redis --dry-run=client -o yaml > redis.yaml

kubectl get pod <pod-name> -o yaml > pod-definition.yaml
``` 

# Kinds

![alt text](images/kinds.png)

## Replication Controller

A ReplicationController ensures that a specified number of pod replicas are running at any one time. In other words, a ReplicationController makes sure that a pod or a homogeneous set of pods is always up and available.
A Deployment that configures a ReplicaSet is now the recommended way to set up replication.

 
## ReplicaSet
A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. Usually, you define a Deployment and let that Deployment manage ReplicaSets automatically.
A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods.










