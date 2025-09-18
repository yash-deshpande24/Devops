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

## Comman Docker Commmands: 
  1. Check running containers:
        - docker ps
  2. Check all containers (running + stopped):
        - docker ps -a
  3. List images:  
        - docker images
  4. Pull a images:
        - docker pull nginx <images name added here>   
---

## Running Containers:
    1 Run Nginx container:
         docker run -itd -p 80:80 nginx
         i - Interactive mode
         t - Allocated terminal
         d - Detached mode
         p 80:80 - maps host port 80 to container on port 80
    2 Run Container with a name:   
          docker run -itd --name --nmae <name added here> -p 80:80 nginx

---          
## Manging Containers:
    1. Enter into a containers:
          docker exec -it <container_id> /bin/bash
    2. Exit from containers:
          exit
    3. Stop containers:
           docker stop <container_id>      
    4. Delete containers:
           docker rm -f <container_id>
    5.Delete images:
           docker rmi <image_id>
---          
           
