# DOCKERS
---
## WHAT IS DOCKER?
    - Dockers is a platforms to builds,share & run application inside container.
    - A containers is a lighweight,portable package that includes everythings needed to run an application.
    - Dockers ensure the application the same way everywhere.
---

## What Dockers Architecture?
    1.Docker client -> send command
    2.Docker Host -> Runs the dockers Daemon (engine that runs managers containers)
    3.Docker Registory -> Store
    4.Docker Images (public/private)
    
 ---  
## How to Install Docker in amazon linux
    sudo yum install docker -y
    sudo systemctl start docker
    sudo systemctl enable docker
    sudo usermod -aG docker ec2-user
    newgrp docker
    sudo chmod 777 /var/run/docker.sock

---    

## How to Install Docker in Ubuntu
    sudo apt install docker.io -y
    sudo systemctl start docker
    sudo systemctl enable docker
    sudo usermod -aG docker ubuntu
    newgrp docker
    sudo chmod 777 /var/run/docker.sock
     
---

### comman Docker Commmands: 
