
from pathlib import Path

# Define the file path
file_path = Path("docker_multistage_notes.md")

# Docker multi-stage notes content with the additional sections
docker_multistage_notes = """# 🐳 Docker Multi-Stage Builds

## 📘 What is Multi-Stage Build?
A **multi-stage Docker build** allows using multiple `FROM` statements in a single Dockerfile.  
Each `FROM` starts a **new stage**, and you can **copy only required files or dependencies** from one stage to another.

This approach helps in creating **smaller, faster, and more secure Docker images**.

---

## 💡 Why Use Multi-Stage Builds?
When building applications, we often need heavy tools and dependencies during build time (like `pip`, `npm`, or compilers).  
However, these are **not required at runtime**.  

So, with **multi-stage builds**, you can:
- Use a **heavy image** for building (Stage 1)
- Use a **lightweight image** for running (Stage 2)

✅ Reduces image size  
✅ Improves performance  
✅ Increases security  

---

## 🧱 Example: Multi-Stage Dockerfile

```dockerfile
# ---------- Stage 1: Builder ----------
# Base image with full Python setup (~1 GB)
FROM python:3.7 AS builder

# Set working directory
WORKDIR /app

# Copy requirements and install dependencies
COPY requirements.txt .
RUN pip install -r requirements.txt

# ---------- Stage 2: Final Image ----------
# Lightweight base image (~140 MB)
FROM python:3.7-slim

# Set working directory
WORKDIR /app

# Copy installed dependencies from builder stage
COPY --from=builder /usr/local/lib/python3.7/site-packages/ /usr/local/lib/python3.7/site-packages/

# Copy remaining project files
COPY . .

# Run the application
ENTRYPOINT ["python", "run.py"]

```
---

## 🧠 Explanation of Dockerfile?

Line	Description
FROM python:3.7 AS builder	Stage 1: Full Python environment for installing dependencies
WORKDIR /app	Sets the working directory inside container
COPY requirements.txt .	Copies dependency list into the container
RUN pip install -r requirements.txt	Installs all Python dependencies
FROM python:3.7-slim	Stage 2: Lightweight Python image (~140 MB)
COPY --from=builder ...	Copies dependencies from Stage 1
COPY . .	Copies your app source code
ENTRYPOINT ["python","run.py"]	Defines container start command
📦 Why Image Size Reduces (1 GB → 140 MB)
Stage	Base Image	Size	Purpose
Builder	python:3.7	~1.04 GB	Full Python + Build tools
Final	python:3.7-slim	~140 MB	Minimal runtime environment

In the final image, only essential runtime dependencies are copied — not temporary build files or pip cache.
That’s why the image size reduces drastically.

---

## 🧰 Useful Commands
Command	Description
docker images	List all built images
docker history <image>	Show image layer sizes
docker rmi <image>	Remove an image
docker run -d -p 5000:5000 flask-app-mini	Run the Flask container

---
