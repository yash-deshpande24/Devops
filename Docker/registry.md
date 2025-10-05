
# 🐳 Docker Registry Notes

## 📘 What is a Docker Registry?
A **Docker Registry** is a storage and distribution system for named Docker images.  
It allows you to **push (upload)** and **pull (download)** container images.

---

## 🏛️ Types of Docker Registries

1. **Docker Hub (Public Registry)**  
   - Default registry provided by Docker.  
   - Anyone can host and share images publicly or privately.  
   - URL: [https://hub.docker.com](https://hub.docker.com)

2. **Private Docker Registry**  
   - Hosted on your local server or cloud instance.  
   - Used for internal image management within organizations.  
   - Example: `registry.mycompany.com`

---

## ⚙️ Commands for Docker Registry

### 🔹 1. Login to Docker Registry
```bash
docker login
```
> Use your Docker Hub or private registry credentials.

For a specific private registry:
```bash
docker login myregistrydomain.com:5000
```

### 🔹 2. Tag an Image
```bash
docker tag local-image:tagname username/repository:tag
```
Example:
```bash
docker tag myapp:latest deshpandeyashrajesh/myapp:v1
```

### 🔹 3. Push Image to Registry
```bash
docker push username/repository:tag
```

### 🔹 4. Pull Image from Registry
```bash
docker pull username/repository:tag
```

### 🔹 5. Run a Local Private Registry
```bash
docker run -d -p 5000:5000 --name registry registry:2
```

### 🔹 6. Tag and Push Image to Private Registry
```bash
docker tag myimage localhost:5000/myimage
docker push localhost:5000/myimage
```

### 🔹 7. Pull Image from Private Registry
```bash
docker pull localhost:5000/myimage
```
## ⚙️ Quick Commands for Docker Registry

### 🔹 Step 1: Login to Docker Registry
```bash
docker login
```
> Use your Docker Hub username and password.

---

### 🔹 Step 2: Tag (Rename) Your Image
```bash
docker tag <local_image_name>:<tag> <dockerhub_username>/<repository_name>:<tag>
```
**Example:**
```bash
docker tag myapp:latest deshpandeyashrajesh/myapp:v1
```
✅ This prepares your image for upload by assigning it a new name (tag).

---

### 🔹 Step 3: Push Image to Docker Hub
```bash
docker push <dockerhub_username>/<repository_name>:<tag>
```
**Example:**
```bash
docker push deshpandeyashrajesh/myapp:v1
```


### 🧰 Helpful Commands
| Command | Description |
|----------|-------------|
| `docker images` | List all images |
| `docker rmi <image>` | Remove an image |
| `docker ps -a` | Show all containers |
| `docker rm <container>` | Remove a container |
| `docker system prune -a` | Remove unused data |

### 🧾 Example Workflow
```bash
docker build -t myapp .
docker tag myapp:latest deshpandeyashrajesh/myapp:v1
docker push deshpandeyashrajesh/myapp:v1
docker pull deshpandeyashrajesh/myapp:v1
docker run -d -p 8080:80 deshpandeyashrajesh/myapp:v1
```

### 📦 Tips
- Always log in before pushing images.
- Use version tags (e.g., `v1`, `v2`) for better version control.
- Use a `.dockerignore` file to skip unnecessary files.
- Secure your private registry with SSL certificates if exposed publicly.
