# DevOps & Interview Q&A

✅ General DevOps Questions

1️⃣ What is DevOps?  
Answer:  
DevOps is a culture and practice where development and operations teams work together to deliver software faster and more reliably. It uses automation, CI/CD, cloud, and monitoring to improve deployment speed and quality.

2️⃣ Why DevOps?  
Answer:  
DevOps helps to release software faster, reduce manual work, improve collaboration, and automate deployment and infrastructure. It increases system reliability and business agility.

3️⃣ Which tools have you used in DevOps?  
Answer:  
- Git & GitHub – Version control  
- Jenkins / GitHub Actions – CI/CD  
- Docker – Containerization  
- Kubernetes (EKS / Minikube) – Orchestration  
- Terraform – Infrastructure as code  
- AWS – EC2, S3, IAM, VPC, RDS, CloudWatch  
- Linux – Shell scripting & server administration  
- Prometheus/Grafana (optional) – Monitoring

---

✅ Linux Questions

4️⃣ Common Linux Commands you use?  
Answer:  
ls, cd, pwd, cp, mv, rm  
top, ps, df -h, free -m  
systemctl for managing services  
Editing files using nano/vim  
Basic scripting for automation

---

✅ Git / GitHub

5️⃣ What is Git and why use it?  
Answer:  
Git is a distributed version control system used to track code changes and collaborate with teams. It helps in versioning, branching, merging, and rollbacks.

6️⃣ CI vs CD?  
Answer:  
- CI (Continuous Integration): Automatically build & test code when developers push changes.  
- CD (Continuous Deployment/Delivery): Automatically deploy code to production or staging environment.

---

✅ CI/CD Pipeline

7️⃣ Explain your CI/CD pipeline  
Answer:  
My pipeline included:  
- Code pushed to GitHub  
- Pipeline triggered in Jenkins  
- Build + Unit tests  
- Docker image created  
- Push to DockerHub  
- Deploy on Kubernetes / EC2  
- Monitor logs in CloudWatch

---

✅ Docker Questions

8️⃣ What is Docker?  
Answer:  
Docker is a tool that packages applications with their dependencies in a container so they run consistently everywhere.

9️⃣ Docker vs Virtual Machine  
Answer:  
Docker — Lightweight, Fast startup, Uses containers  
VM — Heavy, Slow startup, Uses OS-level virtualization

---

✅ Kubernetes (K8s)

🔟 What is Kubernetes?  
Answer:  
Kubernetes is a container orchestration tool that manages containers (scaling, auto-healing, rolling deployments).

11️⃣ Kubernetes Objects you worked with  
Answer:  
Pod, Deployment, Service, ConfigMap, Secret, Namespace

---

✅ Terraform

12️⃣ What is Terraform?  
Answer:  
Terraform is an Infrastructure as Code tool used to automate cloud resource creation using a declarative configuration.

13️⃣ Terraform workflow  
Answer:  
terraform init → plan → apply → destroy

---

✅ AWS Cloud

14️⃣ AWS Services you used  
Answer:  
EC2, S3, IAM, VPC, Subnet, Security Groups, RDS, EBS, CloudWatch, Lambda (basic)

15️⃣ What is VPC?  
Answer:  
VPC is a Virtual Private Cloud — your private network in AWS to launch resources securely.

---

✅ Monitoring

16️⃣ What do you monitor in DevOps?  
Answer:  
Server health (CPU, RAM, Disk), Application logs, Network traffic, Container health, Alerts on failure  
Tools: CloudWatch, Prometheus/Grafana

---

✅ Behavioral Question

17️⃣ How do you handle deployment failure?  
Answer:  
Check logs & pipeline errors, Rollback to previous version, Fix issue and redeploy, Document root cause to avoid future issues

18️⃣ Why do you want DevOps role?  
Answer:  
I like automation and cloud systems. I already have full-stack experience and now hands-on DevOps training, so DevOps suits my skills in CI/CD, cloud, and infrastructure automation.

---

