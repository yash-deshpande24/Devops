
# Docker Projects

## Project: Three Tier Application Docker Compose with Java

### Step 1: Setup Docker
- sudo apt update
- sudo apt install docker.io

### Step 2: Install Docker Compose
- sudo apt install docker-compose -y

### Step 3: Clone Project Repository
- git clone Expense-Tracker-webApp

### Step 4: Project Overview
- Frontend: Thymeleaf (UI based)
- Backend: Spring Boot (Java framework)
- Database: MySQL
- Build tool: Apache Maven (combines frontend & backend)
- Use base Apache Maven image to build frontend & backend
- Connect external databases

### Step 5: Configuration Files to Review
- `/src/main/resources/application.properties`
- `pom.xml` (very important)

### Step 6: Dockerfile Guidance
- Use Maven image first to build app
- Name the builder stage
- Run `mvn` to build app
- Use `openjdk:17-alpine` for runtime

### Step 7: Remove old files
- Remove files before creating new Docker setup:
  - rm -v Dockerfile docker-compose.yml

### Step 8: Dockerfile (multi-stage build)
```Dockerfile
# Stage 1 - Build JAR with Maven
FROM maven:3.8.3-openjdk-17 AS builder

WORKDIR /app

COPY . .

RUN mvn clean install -DskipTests=true

# Stage 2 - Run JAR
FROM openjdk:17-alpine

WORKDIR /app

COPY --from=builder /app/target/*.jar /app/expenseapp.jar

CMD ["java", "-jar", "expenseapp.jar"]
```
- Build image: `docker build -t expenseapp .`
- List images: `docker images`

### Step 9: docker-compose.yml
```yaml
version: "3.8"

services:
  java_app:
    build:
      context: .
    container_name: "expensesapp"
    networks:
      - expenses-app-nw
    environment:
      - SPRING_DATASOURCE_URL=jdbc:mysql://mysql_db:3306/expenses_tracker?allowPublicKeyRetrieval=true&useSSL=false
      - SPRING_DATASOURCE_USERNAME=root
      - SPRING_DATASOURCE_PASSWORD=Test@123
    depends_on:
      mysql_db:
        condition: service_healthy
    ports:
      - "8080:8080"
    restart: always
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost:8080 || exit 1"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 30s

  mysql_db:
    image: mysql:8.0
    container_name: "mysql"
    networks:
      - expenses-app-nw
    environment:
      - MYSQL_ROOT_PASSWORD=Test@123
      - MYSQL_DATABASE=expenses_tracker
    ports:
      - "3306:3306"
    restart: always
    volumes:
      - mysql_data:/var/lib/mysql
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-uroot", "-pTest@123"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 30s

networks:
  expenses-app-nw:

volumes:
  mysql_data:
```
- Start containers: `docker-compose up`
- Build and start containers: `docker-compose up --build`

### Step 10: Remove mysql_data volume
- sudo rm -r mysql_data
- (Preferred Docker command: `docker volume rm mysql_data`)

### Step 11: Rebuild and Start
- docker-compose up --build

### Step 12: Access Application
- Edit security groups, allow TCP 8080 inbound
- Access: `http://<public_ip>:8080`

### Step 13: Nginx Setup
- Copy nginx config from another repo
- Update nginx configuration in `default.conf`
- Add nginx service to `docker-compose.yml`
