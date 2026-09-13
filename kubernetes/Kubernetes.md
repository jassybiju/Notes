# Kubernetes

## What are containers?
Container are an application-centric method to deliver high-performing, scalable applications on any infrastructure of your choice. Containers are best suited to deliver microservices by providing portable, isolated virtual environments for applications to run without interference from other running applications

A **container image** bundles the application along with its runtime, libraries and dependencies, and it represents the source of a container deployed to offer an isolated executable environment for the application.

Container orchestrators are tools which group systems together to form clusters where container's deployment and management is automated at scale while meeting the requirements.

### What features do orchestration tools offer?
- High availability or no downtime
- Scalability or high performance
- Disaster recovery - backup and restore
---
## Kubernetes
**Kubernetes** is an open-source system for automating deployment, scaling, and management of containerized applications
It solves the problem of managin containerized applications at scale by acting as an orchestrator that automates deployment, scaling and lifecycle managemnt

### Features of K8s
- **Automate Bin Packing**
    Kubernetes automatically schedule containers based on resource needs and constraints, to maximize utitlization without sacrificing availability
- **Designed for extensibility**
    A Kubernetes cluster can be extended with new custom features without modifying the upstream source code.
- **Self healing**
    Kubernetes automatically replaces and reschedules containers from failed nodes. It terminates and then restarts container that become unresponsive to health checks, basaed on existing rules/policy. It also prevents traffic from being routing to unresponsive container.

- **Horizontal Scaling**
    Kubernetes scales application manually or automatically based on CPU or custom metrics utilization
- **Service discovery and load balancing**
    Container receive IP addresses from Kubernetes, while it assign a single DBS name to a set of container to aid in load-balancing request from across the container of the set.

- **Automated rollouts and rollbacks**
    Kubernetes seemlessly rollsout and rollsback application updates and configuration changes, constantly monitoring the application's health to prevent any downtimes

- **Secret and configuration management**
    Kubernetes manages sensitive data and configuration details for an application seperately from the container image

### Kubernetes Basic Architecture

At a very high level, K8s is a cluster of compute sytems categorized by their distinct roles:
- One or more control plane nodes / master node
- One or more worker nodes ( optional, but recommneded).
![Components of K8s Cluster](./k8sArch.png)

Control Plane Node runs the following compoents
- **Scheduler** - Responsibile for schduleing containers on different nodes based on the workload and avaible server resources on each node

- **API Server** - Entrypoint to K8s cluster
( ensures Pods placement)
- **etcd** : Key value storage ( Kuberneetes backing store )
- **Container Runtine**
- **Node Agent - Kubelet**
- **Proxy - KubeProxy**
- **Virtual Networks** : It enables communicatin between all the node ( worker and master nodes ) which si the part of the cluster. ( creates one unified machine )
On master nodes important kubernetes processes are running

**Worker Node** provides a running env for client application. These applications are microservices running as application continers .

- Container Runtime
- Node Agent - kubelet
- Proxy - kube-proxy
- Add-ons for DNS, observability components such as dashboards, cluster-level monitoring and logging, and device plugins.

On worker nodes our applications are running

- Each worked node have a kubelet process running one it (it is a kubernetes process that make it possible for cluster to communicate to each other and execute some tasks)
- Each Worker node have docker container of different application deployed on it.
- Controller Manager - Keeps track of whats happening in the cluster
Process running on Master Node

Existing ones are Hardware, OS, 

---

### Kuberenetes Configuration
Its can be installed using different cluster configuration

- **All-in-One Single Node Application**
- **Signle-Control Plane and Multi-Worker installation**
- **Single-Control Plane with Single-Node etcd and Multi-Worker Installation**
- **Multi-Control  and Multi-Worker Installation**
- **Multi-Control with Multi-Node etcd and Multi-Worker Installation**

---

### Kubernetes Basic Concept

Pod : It is the smallest unit that a k8s user interact with. It is a wrapper for container. Each pod is its own self container server. In K8s we only work with the Pods. 

Service : Whenever pods are recreated it gets enw ip. so service stays even after and does the mapping. It has a permanent IP address and acts as a loadbalancer

---

### Kubernetes Config Files
- it tells kubernetes about the different Deployments, Pods and Service ( referred to as 'Objects' ) that we want to create
- Written in YAML Syntax
- Always store these files with our project source code - they are documentation!
- We can create Objects without config files - **do not do this**. Config files provide a precise definition of what your cluster is running

---

### Updating the image Used by a deployment - Method-1

- Make a change in your project code
- Rebuild the image, specifically a new image version
- In the deployment config file, update hte version of the image
- Run the command `kubectl apply -f [depl file name]`

### Update the image used by a deployment - Method -2
- The deployment must be using the `latest` tag in the pod spec section
- Make an update to your code
- Build the image
- Push the image to docker hub
- Run the command kubectl rollout restart deployment [depl-name]

--- 

**Services Provide networking between pods and outside world to pods**

### Types of Services
| | |
|:-----:|:----|
|Cluster IP | Sets ups an easy-to-remember URL to access a pod. Only exposes pods in the cluster|
| Node Port | Makes a pod accessible from *outside the cluster*. Usually only used for dev purposes| 
| Load Balancer | Makes a pod accessible from *outside the cluster*. This is the right way to expose a pod to the outside world|
| External Name| Redirects an in-cluster request to a CNAME url |

### Terminologies on LoadBalancer Service
LoadBalancer Services : Tells kubernetes to reach out to its providers and provision a load balancer. Gets traffic in to a *single pod*. 
Ingree or Ingree Controller : A pod with a set of routing rules to distributre traffic to other services

