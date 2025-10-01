# 🚀 Day 1: Kubernetes & Docker Basics

📅 Date: 23/03/2023  
🧠 Author: Yash Deshpande

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
    docker swarm init
- Containers run in a distributed fashion
- Key components: Pods, Deployments, Services

Sample YAML: Pod Definition
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
____

  
