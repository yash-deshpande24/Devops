# High Availability (HA) in Kubernetes

This document outlines recommended practices to achieve high availability for applications running on Kubernetes. It covers workload types, deployment patterns, service exposure, health checks, scaling, scheduling constraints, storage, and cluster-level considerations.

## Overview

High availability in Kubernetes is achieved by:
- Running multiple copies of application workloads (replicas).
- Distributing replicas across nodes and zones.
- Using Kubernetes Services to load-balance traffic.
- Using health checks to avoid sending traffic to unhealthy pods.
- Using autoscaling, disruption budgets, and scheduling constraints to maintain availability during failures or maintenance.

---

## Workload choices

- Use a **Deployment** for stateless workloads. Deployments provide rolling updates, rollbacks, and easy scaling.
- Use a **StatefulSet** for stateful workloads that require stable network identities or stable persistent storage (e.g., databases).

### Example: Minimal Deployment (stateless)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: web-app
        image: myregistry/web-app:stable
        ports:
        - containerPort: 8080
        readinessProbe:
          httpGet:
            path: /health/ready
            port: 8080
          initialDelaySeconds: 5
          periodSeconds: 10
        livenessProbe:
          httpGet:
            path: /health/live
            port: 8080
          initialDelaySeconds: 15
          periodSeconds: 20
        resources:
          requests:
            cpu: "100m"
            memory: "128Mi"
          limits:
            cpu: "500m"
            memory: "512Mi"
```

### Example: Minimal StatefulSet (stateful)
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: redis
spec:
  serviceName: "redis"
  replicas: 3
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
      - name: redis
        image: redis:7
        ports:
        - containerPort: 6379
        readinessProbe:
          tcpSocket:
            port: 6379
          initialDelaySeconds: 5
          periodSeconds: 10
        volumeMounts:
        - name: data
          mountPath: /data
  volumeClaimTemplates:
  - metadata:
      name: data
    spec:
      accessModes: ["ReadWriteOnce"]
      resources:
        requests:
          storage: 10Gi
```

---

## Services and load balancing
