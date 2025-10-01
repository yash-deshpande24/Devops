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
