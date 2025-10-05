
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

----
