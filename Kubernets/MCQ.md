# K8S Q&A

## 1. What is kubernetes?
Kubernetes is an open-source platform to manage containerized applications

---

## 2. Why you need Kubernetes and what it can do?
1. Service discovery and load balancing 
- Kubernetes can expose a container using the DNS name or using their own IP address.
- If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.

2. Storage orchestration
- Kubernetes can automatically attach storage (local or cloud) to containers, so apps can use data storage easily.

3. Automated rollouts and rollbacks
- Roll-Update: Container can change the actual state to the desired state at a controlled rate.
- Roll-backs: Shift version back version from update version.

4. Automatic bin packing
- Automatic bin packing in Kubernetes is the process of efficiently placing containerized tasks (pods) onto a cluster of nodes. The goal is to optimize resource utilization, such as CPU and memory, by intelligently fitting the "bins" (pods) into the "containers" (nodes).

5.Self-healing
- Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.

6. Horizontal scaling
- Scale your application up and down with a simple command, with a UI, or automatically based on CPU usage.

---

## 3. What is hypervisior and it types?
A hypervisor is software that creates and manages virtual machines (VMs) on a single physical computer.

Types:
- Type 1 (Bare-metal): Runs directly on hardware (e.g., VMware ESXi, Hyper-V).
- Type 2 (Hosted): Runs on top of an operating system (e.g., VirtualBox, VMware Workstation).

---

## 4. difference between Traditional deployment era, Virtualized deployment era, Container deployment era ?

| Feature          | Traditional Deployment   | Virtualized Deployment | Container Deployment                     |
| ---------------- | ------------------------ | ---------------------- | ---------------------------------------- |
| **Isolation**    | None (all apps share OS) | Each VM has its own OS | Each container shares OS but isolated    |
| **Resource Use** | Heavy                    | Moderate               | Light                                    |
| **Startup Time** | Slow (minutes)           | Faster (minutes)       | Very Fast (seconds)                      |
| **Scalability**  | Difficult                | Easier                 | Very Easy                                |
| **Portability**  | Low                      | Medium                 | High                                     |
| **Management**   | Manual                   | With hypervisor        | With container tools (e.g., Docker, K8s) |

---

## 5. What is Cluster and Nodes?
Cluster is group of servers or nodes.

Nodes are called instances.

---

## 6. Components of K8S architecture ?
### Control plane/ Master Node components

1.kube-apiserver
- Designed to scale horizontally—that is, it scales by deploying more instances.
- Communication between server through API server.

2.kube-scheduler
-  Watches for newly created Pods with no assigned node, and selects a node for them to run on.
-  Deploy pod  on worker node.

3.kube-controller-manager
- Check/verify pod running or not.
  
4.ETCD
- Consistent and highly-available key value store used as Kubernetes backing store for all cluster data.

---


### Control plane/ Master Node components 

1.Container runtime
- Empowers Kubernetes to run containers effectively.
- Work for managing the execution and lifecycle of containers.

2.kube-proxy 
- Allow multiple pod to communicate inside or outside of your cluster.

3.kubelet 
- An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
- Send all information of working node to API.

4.Pod
- Packing of containers.

---

## 7. What is Addons?
Addons in Kubernetes are extra tools or components that add special features to the cluster, like DNS, dashboards, or monitoring.

---

## 8. Control plane deployment options ?
| **Method**                 | **Description (Simple Words)**                                               |
| -------------------------- | ---------------------------------------------------------------------------- |
| **Traditional Deployment** | Control plane runs directly on machines or VMs using system services.        |
| **Static Pods**            | Control plane runs as static Pods managed by kubelet (used by kubeadm).      |
| **Self-hosted**            | Control plane runs as Pods inside the cluster, managed by Kubernetes itself. |
| **Managed Services**       | Cloud providers manage the control plane for you (e.g., GKE, EKS, AKS).      |

---

## 9. What are services  and it types?
let you expose your app running on many pods through one fixed endpoint (IP/DNS).

1.ClusterIP
- Expose service on cluster internal IP.
- default service.

2.NodePort
- Range between 30,000 - 32,767.
- Expose service on each Nodes IP (External access).

3.Load Balancer
- Expose service externally usinga external load balancer.

---


## 10. What is Pods ?
Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

Pods are packaging of containers.

---

## 11. What is IntraPod ?
Communication b/w two pods because they share same networks. 

---

## 12. What is Replication Controller?
- A Replication Controller in Kubernetes ensures that a specific number of identical Pods are always running in the cluster.
- Support Only Equality based selector.

---

## 13. What is ReplicaSet ?
- Work same as a Replication Controller.
- Support Equality and Set based selector.

---

## 14. What is d/f b/w rc and rs?
| Replication Controller (RC)            | ReplicaSet (RS)                                |
| -------------------------------------- | ---------------------------------------------- |
| Support equality based selector        | Support eqaulity and set based selector        |
| It is old version                      | It is updated version                          |
| It is less used                        | Mostly used through deployment                 |

---

## 15. What is Labels?
Labels are tags added to Kubernetes objects to identify and organize them.

Are key key-value pairs that are attached to objects such as pod.

---

## 16. What are selctors and it types ?
Selectors are used to find and group objects based on their labels.

Their are two types of selectors:
- 1] Equality-based Selector – Selects objects where the label equals or not equals a value.
- 2] Set-based Selector – Selects objects where the label is in, not in, or exists in a set of values.

---

## 17. What is Deployment?
Deployments manages Pods and ReplicaSet to run a applications.

---

## 18. What is Deployment Strategies?
There is no downtime for our users.

#### 1] Rolling Update Strategy (also Known as Incremental)
- switch to newer version.

#### 2] Rolling Back
- This means that when you roll back to an earlier revision, only the Deployment's Pod template part is rolled back.

#### 3] Blue / Green  Deployments

#### 4] Canary

---

## 18. What is StatefulSets?
- Support persistent storage.
- Manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods.

---

## 19. What is difference b/w statefulSet and Deployment?
| **Deployment**                         | **StatefulSet**                     |
| -------------------------------------- | ----------------------------------- |
| Pods has random name                   | Pods has random name                |
| Support persistent storage per pod     | No persistent storage by default    |
| Used for database related application  | Used for web apps, API's            |
| Pods are created/ deleted in order     | Pods can be created/ deleted any order|


---

## 20. What is DaemonSet?
Pods runs on all nodes to performing task such as a minitoring and logging.

---
## 21. What is Namespaces?
Namespaces provide a mechanism for isolating groups of resources within a single cluster. 

---

## 22. What is volumes 
Kubernetes volumes provide a way for containers in a pod to access and share data via the filesystem. 

---

## 23. Why volumes are important?
1.Data Persistence 
- Containers file are temporary if container stop or crashes the files also deleted.
- Here volume keep data safe even the container  stop or crashes.

2.Shared Storage
- Another problem occurs when multiple containers are running in a Pod and need to share files. It can be challenging to set up and access a shared filesystem across all of the containers.

---

## 23. What is Persistent Volumes?
PV is like a permanent storage which have a lifecycle independent of any individual Pod.

---

## 24. What is  PersistentVolumeClaim?
A PersistentVolumeClaim (PVC) is a request for storage by a user.

---

## 25. What are Access modes in volumes ?
- RWO (ReadWriteOnce) → Read & write by one node (multiple pods allowed if on same node).
- ROX (ReadOnlyMany) → Read-only by many nodes.
- RWX (ReadWriteMany) → Read & write by many nodes.
- RWOP (ReadWriteOncePod) → Read & write by only one Pod in the whole cluster (CSI volumes, K8s v1.22+).

---

## 26. What is ConfigMap?
- A ConfigMap is an API object used to store non-sensitive configuration data.
- Data is store in key-value pairs.

---

## 27. What is Secrets?
- A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key.
- Data is stored in based 64 encoded format.
 
---

## 28. What is Ingress?
An Ingress is an API object that defines rules which allow external access to services in a cluster.

---

## 29. What is Horizontal Pod Autoscaling?
New Pods are created based on observed metrics called HPA.

---

## 30. What is Cluster scaling?
New nodes are created .

---
