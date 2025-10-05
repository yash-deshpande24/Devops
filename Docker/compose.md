
# 🐳 Docker Compose Notes

## 📘 What is Docker Compose?
**Docker Compose** allows you to define and run multi-container Docker applications using a single configuration file (`docker-compose.yml`).  

---

## ⚙️ Key Features
- Manage multiple containers easily  
- Define configurations in YAML  
- Build and run containers with one command  
- Automatically creates networks between services  
- Supports scaling and environment variables  

---

## 🧩 Example docker-compose.yml
```yaml
version: "3.9"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
    depends_on:
      - db
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: mydb
    volumes:
      - db_data:/var/lib/mysql
volumes:
  db_data:
```

---

## 🧰 Common Docker Compose Commands

| Command | Description |
|----------|-------------|
| `docker-compose up` | Start all services |
| `docker-compose up -d` | Start in detached mode |
| `docker-compose down` | Stop and remove services |
| `docker-compose ps` | List running containers |
| `docker-compose logs` | Show logs |
| `docker-compose exec <service>` | Run command inside service |
| `docker-compose build` | Build images |
| `docker-compose restart` | Restart all services |

---

## 🧾 Example Project Structure
```
myapp/
├── docker-compose.yml
├── Backend/
│   ├── Dockerfile
│   └── app.js
└── Frontend/
    ├── Dockerfile
    └── index.html
```

Example `docker-compose.yml`:
```yaml
version: "3.9"
services:
  frontend:
    build: ./Frontend
    ports:
      - "3000:80"
  backend:
    build: ./Backend
    ports:
      - "5000:5000"
    depends_on:
      - db
  db:
    image: postgres
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
    volumes:
      - pg_data:/var/lib/postgresql/data
volumes:
  pg_data:
```

---

## 💡 Tips
- Use `.env` files for environment variables.  
- Use `depends_on` for service order.  
- Use volumes for data persistence.  
- Combine `build` and `image` for flexibility.  
- Use `docker-compose down -v` to remove volumes too.
