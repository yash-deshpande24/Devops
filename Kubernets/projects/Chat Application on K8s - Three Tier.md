# Chat Application on Kubernetes - Three Tier

This guide walks through deploying a **three-tier chat application** (ReactJS frontend, NodeJS backend, MongoDB database) on Kubernetes.

---

## Step 1: Technology Stack

- **Frontend:** ReactJS
- **Backend:** NodeJS
- **Database:** MongoDB

---

## Step 2: Set Up Development Environment

- Open **VS Code**.
- Open terminals for each service.

---

## Step 3: Start Kubernetes Local Cluster

```bash
minikube start --driver=docker
kubectl get nodes
```

---

## Step 4: Create Project Directory and Clone Repo

```bash
cd <your-folder>
git clone https://github.com/yash-deshpande24/full-stack_chatApp.git
```

---

## Step 5: Dockerize Services

- Use Dockerfiles in frontend and backend folders.
- Build Docker images, push to Docker Hub.

### Docker Commands

```bash
docker login -u deshpandeyashrajesh
# password: dckr_pat_6guT02V-lG8WH9MBW4rFzsf9vHs

cd backend
docker build -t deshpandeyashrajesh/chatapp-backend:latest .
docker images
docker push deshpandeyashrajesh/chatapp-backend:latest

cd ../frontend
docker build -t deshpandeyashrajesh/chatapp-frontend:latest .
docker images
docker push deshpandeyashrajesh/chatapp-frontend:latest
```

> **Tip:**  
> Change name/tag:  
> `docker image tag <old> <new>`

- Use official MongoDB image from Docker Hub.

---

## Step 6: Create Kubernetes Resources

### 1. Namespace

`namespace.yml`
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: chat-app
```
```bash
kubectl create -f namespace.yml
kubectl get ns
```

---

### 2. Deployments

#### Backend Deployment

`backend-deployment.yml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-deployment
  namespace: chat-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      name: backend-pod
      namespace: chat-app
      labels:
        app: backend
    spec:
      containers:
      - name: chat-app-backend
        image: deshpandeyashrajesh/chatapp-backend:latest
        ports:
        - containerPort: 5001
        env:
        - name: NODE_ENV
          value: production
        - name: MONGO_URL
          value: "mongodb://mongodbadmin:secret@mongodb:27017/chatapp/dbname?authSource=admin"
        - name: JWT_SECRET
          valueFrom:
            secretKeyRef:
              name: chat-app-secrets
              key: jwt
        - name: PORT
          value: "5001"
```

#### Frontend Deployment

`frontend-deployment.yml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-deployment
  namespace: chat-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      name: frontend-pod
      namespace: chat-app
      labels:
        app: frontend
    spec:
      containers:
      - name: chat-app-frontend
        image: deshpandeyashrajesh/chatapp-frontend:latest
        ports:
        - containerPort: 80
        env:
        - name: NODE_ENV
          value: production
```

#### MongoDB Deployment

`mongodb-deployment.yml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodb-deployment
  namespace: chat-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      name: mongodb-pod
      namespace: chat-app
      labels:
        app: mongodb
    spec:
      containers:
      - name: chat-app-mongodb
        image: mongo:latest
        ports:
        - containerPort: 27017
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          value: mongodbadmin
        - name: MONGO_INITDB_ROOT_PASSWORD
          value: secret
        volumeMounts:
        - name: mongodb-data
          mountPath: /data/db
      volumes:
      - name: mongodb-data
        persistentVolumeClaim:
          claimName: mongodb-pvc
```

---

### 3. Persistent Volume & Claim

`mongodb-pv.yml`
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mongodb-pv
  namespace: chat-app
spec:
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 5Gi
  hostPath:
    path: /data
```

`mongodb-pvc.yml`
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongodb-pvc
  namespace: chat-app
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

---

### 4. Services

`mongodb-service.yml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mongodb
  namespace: chat-app
spec:
  selector:
    app: mongodb
  ports:
  - port: 27017
    targetPort: 27017
```

`backend-service.yml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend
  namespace: chat-app
spec:
  selector:
    app: backend
  ports:
  - port: 5001
    targetPort: 5001
```

`frontend-service.yml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: frontend
  namespace: chat-app
spec:
  selector:
    app: frontend
  ports:
  - port: 80
    targetPort: 80
```

---

### 5. Secrets

`secrets.yml`
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: chat-app-secrets
  namespace: chat-app
type: Opaque
data:
  jwt: MDBjNzAwMTM1NDI3ZWU5NDQ3NTgzY2IzNzA5NDY4MDYK
```
> **Note:**  
> Use `echo -n "your_jwt_secret" | base64` to encode your secret.

---

## Step 7: Apply Kubernetes Files

```bash
kubectl apply -f mongodb-pv.yml
kubectl apply -f mongodb-pvc.yml
kubectl apply -f secrets.yml
kubectl apply -f mongodb-deployment.yml
kubectl apply -f mongodb-service.yml
kubectl get pods -n chat-app
kubectl get svc -n chat-app

kubectl apply -f backend-deployment.yml
kubectl apply -f backend-service.yml

kubectl apply -f frontend-deployment.yml
kubectl apply -f frontend-service.yml
```

---

## Step 8: Troubleshooting Pods

- Use `kubectl get pods -n chat-app` to check pod status.
- Use `kubectl describe pod <pod-name> -n chat-app` for details/errors.
- Use `kubectl logs <pod-name> -n chat-app` to check logs.

---

## Step 9: Port Forwarding

```bash
kubectl get svc -n chat-app
kubectl port-forward service/backend -n chat-app 5001:5001 &
kubectl port-forward service/frontend -n chat-app 80:80 &
```
If required:
```bash
sudo -E kubectl port-forward service/frontend -n chat-app 80:80
# password: test@123
```

---

## Step 10: Access Application

- Open browser:
  - [http://localhost:80](http://localhost:80) - Frontend
  - [http://localhost:5001](http://localhost:5001) - Backend API

---

## Step 11: Debugging Common Errors

- If error on account creation: "localhost API auth file not found"  
  > **Reason:** Backend may not be connected to MongoDB.  
  - Check backend deployment and environment variables (`MONGO_URL`, `JWT_SECRET`).
  - Check secrets and service connectivity.
  - Use `kubectl logs backend-deployment-<id> -n chat-app` for mongoose errors.

---

## Step 12: Verify & Chat

- After successful setup and port-forwarding, create an account and start chatting.

---

## Step 13: Ingress Setup

To expose your services via a domain, create an ingress resource:

`ingress.yml`
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: chatapp-ingress
  namespace: chat-app
  labels:
    name: myingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
spec:
  rules:
  - host: chat-tws.com
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: frontend
            port: 
              number: 80
      - pathType: Prefix
        path: "/api"
        backend:
          service:
            name: backend
            port: 
              number: 5001      
```

Apply and verify ingress:
```bash
kubectl apply -f ingress.yml
kubectl get ing -n chat-app
kubectl get ns 
```

If using Minikube, enable ingress addon:
```bash
minikube addons enable ingress
```

---

## References

- [full-stack_chatApp GitHub repo](https://github.com/yash-deshpande24/full-stack_chatApp)
