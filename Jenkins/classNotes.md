# Jenkins & CI/CD Pipeline Notes

## Episode 1
**Date:** 2024/10/25

### Source Check
- Jenkins UI accessible at: `15:8080`

### Notes
- Jenkins home directory: `/var/jenkins`
- Steps to set up:
  - Use `cat < >` to copy content
  - Install
  - Save
  - Start

### Question
- 30/10/25

### Key Points
- Jenkins is a free open-source automation tool used to build, test, and deploy software automatically.

### Instance Setup
- OS: Ubuntu AMI
- Port: 8080
- Size: 20GB

### Installation
- Install Java and Jenkins

---

## Build and Cleanup
**Date:** [Not Specified]

### Actions
- Build Now and check `19:8089`
- Delete `Centa.no`

### Notes
- `delete` is a new code (repeated)

### Pipeline Outline
1. Defaults
2. Move structured and hierarchical syntax
3. Pipeline
   - Agent or stage
   - Stage 1.1
   - Stage 1.2

### Results Types
- Based on **Groovy scripting language**
- Example:
  - `node`
  - `stage('code')`
  - `zip 'num install'`

---

## Manual Approach
**Date:** [Not Specified]

### Steps
1. Clone Git repository
2. Build using Maven
3. Deploy on Docker container

### Step 1: Launch Instance
- AMI: Ubuntu
- Port: 8080
- Size: 20GB

### Step 2: Install Jenkins & Setup
```bash
git clone https://... ProjectInstanceMerge
ls
cd Project-InstanceMerge
ls
mvn clean package
ls
cd target
ls
```

# Jenkins + Docker + SonarQube — Full Setup (Ubuntu 24.04 on AWS EC2)

Short, actionable guide: corrected Jenkins pipeline, server Docker setup, SonarQube notes, and Jenkins credentials steps. Use "$BROWSER" <url> to open web UI from the dev container host.

---

## Prerequisites (EC2)
- AMI: Ubuntu 24.04 LTS
- Instance type: t2.medium
- Root storage: 20 GB (or 25 GB for Sonar)
- Key pair: downloaded `.pem`
- Security Group inbound:
  - SSH (22) from your IP
  - Jenkins (8080) from your IP
  - App port (example 8088) from your IP
  - SonarQube (9000) from your IP (if Sonar on EC2)

---

## Docker on the server (Jenkins agents or local runs)
Run on the Ubuntu VM (replace `jenkins`/`ubuntu` user names as needed):
```bash
sudo apt update
sudo apt install -y docker.io
# add users to docker group for non-root docker usage
sudo usermod -aG docker jenkins
sudo usermod -aG docker ubuntu
# lightweight (insecure) permission for demo only; prefer correct group ownership in production
sudo chmod 777 /var/run/docker.sock
# verify
docker --version
```

Note: granting 777 to docker.sock is insecure — use it only for quick demos. Best practice: add Jenkins user to `docker` group and restart Jenkins.

---

## SonarQube (Docker) — quick run (if using docker for Sonar)
- Expose port 9000 in SG.
- Run SonarQube via Docker (example):
```bash
docker run -d --name sonarqube -p 9000:9000 \
  -e SONAR_JDBC_USERNAME=sonar -e SONAR_JDBC_PASSWORD=sonar \
  sonarqube:lts
```
- Open Sonar UI: $BROWSER http://<SONAR_IP>:9000
- Default login: admin / admin
- Generate token: My Account → Security → Generate Token

---

## Jenkins credentials to add
- Secret Text: SONAR_TOKEN (value = Sonar generated token)
- Username/password: DOCKER_REGISTRY (username + password) if pushing images
- (Optional) AWS credentials or IAM role for ECR/S3 access

---

## Corrected Declarative Jenkins Pipeline (Jenkinsfile)
- This pipeline uses Maven tool named `maven-3` configured in Jenkins -> Global Tool Configuration.
- It runs Sonar analysis using SONAR_TOKEN stored as Jenkins Secret Text.

```groovy
// filepath: Jenkinsfile
pipeline {
  agent any
  tools {
    maven 'maven-3'
  }
  environment {
    SONAR_TOKEN = credentials('SONAR_TOKEN')   // secret text credential id in Jenkins
    DOCKER_REG = 'myregistry.example.com'      // change if using registry
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh 'mvn -B clean package'
      }
    }

    stage('SonarQube Analysis') {
      steps {
        withEnv(["SONAR_HOST_URL=http://sonar:9000"]) {
          sh "mvn -B sonar:sonar -Dsonar.login=${SONAR_TOKEN} -Dsonar.host.url=${SONAR_HOST_URL}"
        }
      }
    }

    stage('Docker Build') {
      steps {
        script {
          def img = "myapp:${env.BUILD_NUMBER ?: 'local'}"
          sh "docker build -t ${img} ."
          // optional push (requires docker login credential configured or IAM role)
          // withCredentials([usernamePassword(credentialsId: 'DOCKER_REG_CRED', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          //   sh "echo $DOCKER_PASS | docker login ${DOCKER_REG} -u $DOCKER_USER --password-stdin"
          //   sh "docker tag ${img} ${DOCKER_REG}/${img}"
          //   sh "docker push ${DOCKER_REG}/${img}"
          // }
        }
      }
    }

    stage('Run Container (smoke)') {
      steps {
        sh '''
          docker rm -f ct || true
          docker run -d --name ct -p 8088:8081 myapp:${BUILD_NUMBER}
        '''
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
      junit 'target/surefire-reports/*.xml'
    }
  }
}
```

Notes:
- Update `DOCKER_REG` and credential IDs for your environment.
- If Jenkins runs in Kubernetes or agent containers, install Docker inside the agent or use Docker-in-Docker patterns / Docker socket mounting with caution.

---

## Jenkins configuration pointers
1. Tools:
   - Jenkins → Manage Jenkins → Global Tool Configuration → Add Maven installation named `maven-3`.
2. SonarQube:
   - Jenkins → Manage Jenkins → Configure System → SonarQube servers
   - Add server name `sonar-server` and URL `http://sonar:9000` (or actual Sonar IP).
   - Authentication: use generated token (SONAR_TOKEN).
3. Credentials:
   - Add Secret Text credential with id `SONAR_TOKEN`.
   - Add username/password credential for Docker registry if required (id used in pipeline).
4. Nodes:
   - If using Docker on controller, ensure Jenkins user is in `docker` group and Jenkins restarted.

---

## Final steps and checks
- Restart Jenkins if you changed group membership:
```bash
sudo systemctl restart jenkins
```
- Open Jenkins UI: $BROWSER http://<EC2_PUBLIC_IP>:8080
- Trigger pipeline (create new Pipeline job; point to repo with Jenkinsfile).
- Visit SonarQube: $BROWSER http://<SONAR_HOST_IP>:9000
- Verify container app: $BROWSER http://<EC2_PUBLIC_IP>:8088

---

## Troubleshooting (quick)
- Jenkins logs: sudo journalctl -u jenkins -f
- Docker permission issues: check `groups jenkins` and restart Jenkins
- Port conflicts: sudo ss -ltnp | grep LISTEN
- Sonar analysis fails: confirm SONAR_TOKEN and URL, run `mvn sonar:sonar -X` for verbose logs

---

If you want, I can:
- Add a sample `nginx` reverse-proxy config for Jenkins with LetsEncrypt.
- Generate a cloud-init user-data script to provision Jenkins + Docker + Sonar automatically.
```// filepath: /workspaces/Devops/jenkins-aws-setup.md

# Jenkins + Docker + SonarQube — Full Setup (Ubuntu 24.04 on AWS EC2)

Short, actionable guide: corrected Jenkins pipeline, server Docker setup, SonarQube notes, and Jenkins credentials steps. Use "$BROWSER" <url> to open web UI from the dev container host.

---

## Prerequisites (EC2)
- AMI: Ubuntu 24.04 LTS
- Instance type: t2.medium
- Root storage: 20 GB (or 25 GB for Sonar)
- Key pair: downloaded `.pem`
- Security Group inbound:
  - SSH (22) from your IP
  - Jenkins (8080) from your IP
  - App port (example 8088) from your IP
  - SonarQube (9000) from your IP (if Sonar on EC2)

---

## Docker on the server (Jenkins agents or local runs)
Run on the Ubuntu VM (replace `jenkins`/`ubuntu` user names as needed):
```bash
sudo apt update
sudo apt install -y docker.io
# add users to docker group for non-root docker usage
sudo usermod -aG docker jenkins
sudo usermod -aG docker ubuntu
# lightweight (insecure) permission for demo only; prefer correct group ownership in production
sudo chmod 777 /var/run/docker.sock
# verify
docker --version
```

Note: granting 777 to docker.sock is insecure — use it only for quick demos. Best practice: add Jenkins user to `docker` group and restart Jenkins.

---

## SonarQube (Docker) — quick run (if using docker for Sonar)
- Expose port 9000 in SG.
- Run SonarQube via Docker (example):
```bash
docker run -d --name sonarqube -p 9000:9000 \
  -e SONAR_JDBC_USERNAME=sonar -e SONAR_JDBC_PASSWORD=sonar \
  sonarqube:lts
```
- Open Sonar UI: $BROWSER http://<SONAR_IP>:9000
- Default login: admin / admin
- Generate token: My Account → Security → Generate Token

---

## Jenkins credentials to add
- Secret Text: SONAR_TOKEN (value = Sonar generated token)
- Username/password: DOCKER_REGISTRY (username + password) if pushing images
- (Optional) AWS credentials or IAM role for ECR/S3 access

---

## Corrected Declarative Jenkins Pipeline (Jenkinsfile)
- This pipeline uses Maven tool named `maven-3` configured in Jenkins -> Global Tool Configuration.
- It runs Sonar analysis using SONAR_TOKEN stored as Jenkins Secret Text.

```groovy
// filepath: Jenkinsfile
pipeline {
  agent any
  tools {
    maven 'maven-3'
  }
  environment {
    SONAR_TOKEN = credentials('SONAR_TOKEN')   // secret text credential id in Jenkins
    DOCKER_REG = 'myregistry.example.com'      // change if using registry
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        sh 'mvn -B clean package'
      }
    }

    stage('SonarQube Analysis') {
      steps {
        withEnv(["SONAR_HOST_URL=http://sonar:9000"]) {
          sh "mvn -B sonar:sonar -Dsonar.login=${SONAR_TOKEN} -Dsonar.host.url=${SONAR_HOST_URL}"
        }
      }
    }

    stage('Docker Build') {
      steps {
        script {
          def img = "myapp:${env.BUILD_NUMBER ?: 'local'}"
          sh "docker build -t ${img} ."
          // optional push (requires docker login credential configured or IAM role)
          // withCredentials([usernamePassword(credentialsId: 'DOCKER_REG_CRED', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          //   sh "echo $DOCKER_PASS | docker login ${DOCKER_REG} -u $DOCKER_USER --password-stdin"
          //   sh "docker tag ${img} ${DOCKER_REG}/${img}"
          //   sh "docker push ${DOCKER_REG}/${img}"
          // }
        }
      }
    }

    stage('Run Container (smoke)') {
      steps {
        sh '''
          docker rm -f ct || true
          docker run -d --name ct -p 8088:8081 myapp:${BUILD_NUMBER}
        '''
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
      junit 'target/surefire-reports/*.xml'
    }
  }
}
```

Notes:
- Update `DOCKER_REG` and credential IDs for your environment.
- If Jenkins runs in Kubernetes or agent containers, install Docker inside the agent or use Docker-in-Docker patterns / Docker socket mounting with caution.

---

## Jenkins configuration pointers
1. Tools:
   - Jenkins → Manage Jenkins → Global Tool Configuration → Add Maven installation named `maven-3`.
2. SonarQube:
   - Jenkins → Manage Jenkins → Configure System → SonarQube servers
   - Add server name `sonar-server` and URL `http://sonar:9000` (or actual Sonar IP).
   - Authentication: use generated token (SONAR_TOKEN).
3. Credentials:
   - Add Secret Text credential with id `SONAR_TOKEN`.
   - Add username/password credential for Docker registry if required (id used in pipeline).
4. Nodes:
   - If using Docker on controller, ensure Jenkins user is in `docker` group and Jenkins restarted.

---

## Final steps and checks
- Restart Jenkins if you changed group membership:
```bash
sudo systemctl restart jenkins
```
- Open Jenkins UI: $BROWSER http://<EC2_PUBLIC_IP>:8080
- Trigger pipeline (create new Pipeline job; point to repo with Jenkinsfile).
- Visit SonarQube: $BROWSER http://<SONAR_HOST_IP>:9000
- Verify container app: $BROWSER http://<EC2_PUBLIC_IP>:8088

---

## Troubleshooting (quick)
- Jenkins logs: sudo journalctl -u jenkins -f
- Docker permission issues: check `groups jenkins` and restart Jenkins
- Port conflicts: sudo ss -ltnp | grep LISTEN
- Sonar analysis fails: confirm SONAR_TOKEN and URL, run `mvn sonar:sonar -X` for verbose logs

---

If you want, I can:
- Add a sample `nginx` reverse-proxy config for Jenkins with LetsEncrypt.
- Generate a cloud-init user-data script to provision Jenkins + Docker + Sonar automatically.

---

# Jenkins & DevOps Class Notes

## Jenkins Setup

### 1. Conduite: `id = posmed = admin`

#### Create Token:
- Go to: A data → any account → security → generate token

---

### Step 5: Instructions

#### Instruction:
1. Either tense or not
2. Which is the word?
3. What does some reason?

---

### Test Configuration:
1. **Add JDK**
   - Name: `jdk17`
   - Install from: adoption.net
   - Version: 17

2. **Add Benevolue Scanner**
   - Name: `genox-accessos`

3. **Add Nodes**
   - Name: `node16`
   - Version: 16

4. **Add Docker**

---

## Step 6: Credentials

### Global Credentials:
- Global → Add credentials
- Reset text
- `id = doersp = zeros-token`
- `secret = pairs_token`

### Add Credentials and Data:
- None: `doctor-usman`
- Password ↔
- `id = doersp = doctor-used`

### Manage Testing → Testing:
- Environment variables
- None: `/cona-sense`
- User
- `token = data + sense_token`

---

## Step 7: Retat
- `switch = return`

---

## Step 8: New Item
- Name: `netflix → prepare`
- Pipeline script: Paste from pipeline setup

**Note:** Change Repo & image name

---

## Step 9: Buchliste

| Name | FJ | Resume / found & initial | +ner Agoin |
|------|-----|--------------------------|------------|
|      |     | Consolidated             |            |

---

## Step 10: Check
- Check `1p:8081`

---

## Infrastructure Setup

### Instance Creation (Step 1):
- Ubuntu instance
- All traffic allowed
- 30 GB storage
- t2 large instance type

### Step 2: Connect the instance

### Services to Install:
- Create similar UI: ❌ counter database @ container
- Install Node.js
- Install Docker
- Install SonarQube

### Port Checks:
- Check `ip:8080` (Node)
- Check `ip:9000` (SonarQube)

### EKS Configuration:
- Change version: 1.33
- Configure Region
- Instance sizes: large, small

---

## Pipeline Notes

### Pipeline Changes:
- Change procedure
- Change environment
- Build Now

### Important Notes:
- If paused, there is no image and it is not displayed

---

## Kubernetes & ArgoCD

### Step 6 - Kubernetes Operations:
- Work with nodes
- Create a namespace
- Apply ArgoCD
- Wait 2-3 minutes
- Check pods → argoed → add user

### ArgoCD Setup:
- argoed → add user
- ad ad user

---

## Helm Notes

### Helm Definition:
- Helm is a package manager in Kubernetes
- Helm is used to deploy, manage, and applications on Kubernetes

---

## Miscellaneous Notes

### Date Formats:
- Multiple dates mentioned throughout notes
- Format: `c/11/25` and others

### Language Notes:
- Mix of English, French, and Arabic technical terms
- Various technical concepts and configurations

### Project Checks:
- Destination: `#detd "dat"`
- Nomogacé: dragon à
- Gest click & check project
- Siège II: En sauve

### Kubernetes Commands:
- `kubect1 get pods`
- `kubect1 get ave`
- Check link ✓
