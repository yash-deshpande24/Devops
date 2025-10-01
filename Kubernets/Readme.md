# 🚀 Day 1

---

## 📌 Overview

This document summarizes foundational concepts in containerization and orchestration using **Docker** and **Kubernetes**. It covers environment differences, architectural styles, Docker Swarm basics, and a sample Kubernetes YAML configuration.

---

## 🧪 Environments: Dev vs Test vs Prod

| Environment | Purpose | Characteristics |
|------------|---------|------------------|
| Development | Code writing & debugging | Frequent changes, local setup |
| Testing     | Validate functionality   | Simulates production, automated tests |
| Production  | Live user environment    | Stable, secure, monitored |

---

## 🧱 Monolithic vs Microservices

| Architecture | Description | Pros | Cons |
|--------------|-------------|------|------|
| Monolithic   | Single codebase, tightly coupled | Simple deployment | Hard to scale, fragile |
| Microservices| Independent services communicating via APIs | Scalable, flexible | Complex deployment, requires orchestration |

---

## 🔄 Reusable Components in Full Stack

- Create shared modules (e.g., auth, logging)
- Use container images for consistent environments
- Deploy via CI/CD pipelines across frontend, backend, and services

---

## 🐳 Docker Essentials

### Docker Image → Container

- **Image**: Blueprint of the application
- **Container**: Running instance of the image

### DockerHub

- Public registry to **push** and **pull** Docker images  
  Example:  
  ```bash
  docker push yashdeshpande/yoga

## What is Docker Swam
- Native clustering tool for Docker
- Manages multiple containers across nodes
- Initialization:
   ```bash
    docker swarm init
- Containers run in a distributed fashion
- Key components: Pods, Deployments, Services

## Sample YAML: Pod Definition
```bash
apiVersion: v1
kind: Pod
metadata:
  name: pod1
spec:
  containers:
    - name: yashdeshpande
      image: yashdeshpande/yoga
      ports:
        - containerPort: 80
```
## Difference Between Docker Swarm and Kubernetes

| Feature | Docker Swarm | Kubernetes |
| :--- | :--- | :--- |
| Installation & Setup | Simple and integrated with Docker Engine | More complex, separate CLI, steeper learning curve |
| Application Deployment | Uses YAML or Docker Compose | Flexible with pods, deployments, namespaces |
| Scaling | Quick scaling but no automatic scaling | Automatic scaling, self-healing |
| High Availability | Duplicate services and reschedule containers | Advanced fault tolerance, rolling updates |
| Monitoring | Requires third-party tools | Built-in and third-party integration |
| Security | TLS for node communication and access control | RBAC, SSL/TLS, and advanced security features |
| Load Balancing | Built-in automatic load balancing using DNS | Requires integrations like Nginx Ingress |
| Networking | Overlay network for secure cross-host communication | Each pod gets unique IP, shared network namespace |
___

# Days 2
---

### What is Kubernetes?
- Nodes = Instances
- Kubernetes is an open-source platform developed by Google.
  
### Why do we need Kubernetes?
- Container management: running 1-2 containers
- High Availability - Restarts
- Scalability - Increase or decrease
- Load balancing: user traffic across
- Portability - Run anywhere
- Automation - deployment, rollback, update made easy

  ### What is Kubernetes Architecture?
- Controls plan make decisions
- Worker nodes run your apps
<img width="2048" height="2048" alt="image" src="https://github.com/user-attachments/assets/2f998b77-7c25-479d-8ae2-1202a9d5be19" />

### How to be use Kubernetes?
1. Kubernetes cluster:
  - minikube (single K8s cluster) - practice
  - kubeadm (multi node K8s cluster)

2. Cloud:
  - AWS: EKS
  - Azure: AKS
  - GCP: GKE

3. Kind cluster (practice)
  - Killercoda free web based practice

### Open a website of Killercoda
  - Select option Playgrounds
  - Select Kubernetes 1.33

Commands:
  - `kubectl get nodes`
  - `kubectl get node -o wide`
  - Create pods
    - `kubectl run pod-1 --image=nginx`
  - List command
    - `kubectl get pods`
  - Pods command in detail
    - `kubectl get pods -o wide`
  - Show description about pod
    - `kubectl desc pod pod-1`
    - `kubectl describe pod pod-1`
  - When we login under a pod's commands:
    - `kubectl exec -it pod-1 bash`
    - exit
## Lock check
  - `kubectl logs pod prod-1`

## Services
  1) cluster ip (default service)
  2) nodeport (instance ip)
  3) load balances (different pods to be access/external access)

1) cluster IP + through access :-
  - `kubectl expose pod prod-1`
  - `port = 80, target-port = 80`
  - `type = ClusterIP`
  - `kubectl get pods`
  - `kubectl get svc`
  - `kubectl exec -it pod-1 -- curl <ip-address>`

2) NodePort
  - `kubectl run prod-blue --image= abhipraydh96/blue`
  - `kubectl get pods`
  - `kubectl expose pod --port=80 --target-port=80 --type=nodeport`
  - `kubectl get svc`
---    
          
Day3 
---

## Kubernetes Advantages

Kubernetes is a powerful container orchestration platform with several key benefits [8]:

*   **Self-Healing**: Kubernetes automatically restarts containers that fail, replaces and reschedules containers when nodes die, and kills containers that don't respond to user-defined health checks. This ensures application uptime without manual intervention.
*   **Scalability**: You can scale your application up or down with a simple command, or automatically based on CPU usage. This allows your application to adapt to changing workloads seamlessly.
*   **Load Balancing**: Kubernetes can automatically distribute network traffic across multiple container instances, ensuring that the workload is spread evenly and preventing any single instance from being overloaded.

---

## Amazon EKS

---
**Amazon Elastic Kubernetes Service (EKS)** is a managed service from AWS that makes it easy to run Kubernetes without needing to install and operate your own Kubernetes control plane [1].

*   **What it does**: EKS manages the Kubernetes control plane (the "brain" of the cluster) for you across multiple AWS availability zones to ensure high availability.
*   **Why it's useful**: It handles complex tasks like patching, node provisioning, and updates, allowing you to focus on building and deploying your applications instead of managing infrastructure [1].

---

## Understanding YAML Files
---

In Kubernetes, you define all your objects and application configurations in YAML files. These files describe the *desired state* of your system [8].

### Key Kubernetes Objects

---
*   **Pod**: The smallest and most basic deployable object in Kubernetes. It represents a single instance of your application and can hold one or more containers.
*   **ReplicaSet**: Ensures that a specified number of pod replicas are running at any given time. Its main job is to maintain a stable set of pods.
*   **Deployment**: A higher-level object that manages ReplicaSets and provides declarative updates to applications. This is the most common way to deploy a stateless application. It handles rolling updates and rollbacks gracefully.
*   **Service**: An abstract way to expose an application running on a set of Pods as a network service. It provides a stable IP address and DNS name, and load balances traffic to the pods it targets.

---
  ````
vim pod.yaml
````

````
apiVersion: v1 
kind: Pod 
metadata: 
  name: pod-yoga 
  labels:
    app: yoga
spec: 
  containers:
   - name: c1 
     image: abhipraydh96/yoga 
     ports:
      - containerPort: 80

---
apiVersion: v1 
kind: Service 
metadata: 
  name: svc-yoga 
spec:
  selector: 
    app: yoga 
  ports:
   - port: 80
     protocol: "TCP"
     targetPort: 80
  type: ClusterIP
````

````
kubectl apply -f pod.yaml
````
````
kubectl get pods
kubectl get svc
kubectl exec -it pod-yoga -- curl <clusterip>
````
---
*   kind: Pod: Specifies that we are creating a Pod.
*   metadata: Contains the name and labels for the Pod. Labels are used to identify and group objects.
*   spec.containers: A list of containers to run in the Pod. Here, we define one container using the nginx image.

---
## Common Kubectl Commands
---
kubectl is the command-line tool for interacting with a Kubernetes cluster. Here are some essential commands:

| Command                               | Description                                                              |
| ------------------------------------- | ------------------------------------------------------------------------ |
| kubectl apply -f <filename>.yaml    | Creates or updates resources from a YAML file.                           |
| kubectl get pods                    | Lists all pods in the current namespace.                                 |
| kubectl get svc                     | Lists all services in the current namespace.                             |
| kubectl logs <pod-name>             | Displays the logs from a container in a pod. Essential for debugging.    |
| kubectl exec -it <pod-name> -- /bin/bash | Opens an interactive shell inside a running container for debugging. |
| kubectl describe pod <pod-name>     | Shows detailed information about a specific pod, including events.       |
| kubectl delete -f <filename>.yaml   | Deletes the resources defined in a YAML file.                            |

---
