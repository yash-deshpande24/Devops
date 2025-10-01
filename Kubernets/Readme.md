# 🚀 Day 1: Kubernetes & Docker Basics

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
          
