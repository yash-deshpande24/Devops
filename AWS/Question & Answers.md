# AWS EC2, CloudWatch & Auto Scaling Guide

## 🖥️ Amazon EC2 (Elastic Compute Cloud)

### 🧠 What is EC2?

EC2 (Elastic Compute Cloud) is a service that allows you to run virtual servers (called instances) in the cloud.

You can think of it as renting a computer from AWS that you can use to:
- Host websites or apps
- Run background jobs
- Store and process data
- Experiment with code or machine learning models

You control how much CPU, memory, and storage you want — and you pay only for what you use.

### ⚙️ Simple Example

Imagine you want to host a website. Instead of buying a physical server, you:
1. Go to the AWS console
2. Launch an EC2 instance (like creating a virtual machine)
3. Choose an operating system (e.g., Ubuntu, Windows)
4. Connect using SSH or RDP
5. Install your web server (e.g., Apache or Nginx)

Your website is now live — all in the cloud 🌐

### 🧩 Key Features

| Feature | Description |
|---------|-------------|
| **Elastic** | You can increase or decrease instances anytime. |
| **Scalable** | Easily handle traffic spikes by adding more instances. |
| **Pay-as-you-go** | Only pay for the time your instance runs. |
| **Customizable** | Choose OS, CPU, memory, storage, and network. |
| **Secure** | Uses key pairs, firewalls (security groups), and IAM roles. |

### ❓ Common EC2 Interview Questions & Answers

#### Q1. What is an EC2 instance?
**👉** It's a virtual server in AWS used to run applications.

#### Q2. What are EC2 instance types?
**👉** AWS provides many instance types based on usage:
- **General Purpose** (t2, t3) – balanced CPU and memory
- **Compute Optimized** (c5, c6) – more CPU power
- **Memory Optimized** (r5, r6) – more RAM for large data
- **Storage Optimized** (i3, d2) – high disk performance
- **Accelerated Computing** (p3, g4) – for ML or GPU workloads

#### Q3. What are the different EC2 pricing models?
**👉**
- **On-Demand**: Pay per hour or second — no long-term contract.
- **Reserved Instances**: Commit for 1 or 3 years — cheaper.
- **Spot Instances**: Unused EC2 capacity — up to 90% cheaper, but can be interrupted.
- **Dedicated Hosts**: Physical servers dedicated to you.

#### Q4. What is an AMI (Amazon Machine Image)?
**👉** AMI is a template used to launch EC2 instances. It includes:
- Operating system
- Application server
- Any pre-installed software

#### Q5. What is an Elastic IP?
**👉** It's a static public IP address that you can attach to your EC2 instance — it doesn't change even if you restart the instance.

#### Q6. What are Security Groups in EC2?
**👉** They act like firewalls — controlling inbound and outbound traffic to your instance.

**Example:**
- Allow port 22 (SSH) for Linux access
- Allow port 80/443 for web traffic

#### Q7. What is the difference between Stop, Terminate, and Reboot?

| Action | Description |
|--------|-------------|
| **Stop** | Instance shuts down but root volume is kept. You can start it later. |
| **Terminate** | Instance is permanently deleted. |
| **Reboot** | Simply restarts the instance. |

#### Q8. What is the use of EC2 Key Pair?
**👉** A key pair (private & public key) is used to securely connect to your instance (via SSH for Linux or RDP for Windows).

### 💡 Real-World Use Cases
- Hosting websites or APIs
- Running backend servers for mobile apps
- Batch processing or data analysis

## 📊 Amazon CloudWatch

### 🧠 What is CloudWatch?

CloudWatch is a monitoring service for AWS. It helps you track and visualize:
- CPU usage
- Memory
- Disk and network performance
- Custom app metrics
- Logs

Basically, it tells you: "How healthy are your EC2 instances or AWS services?"

### ⚙️ How CloudWatch Works

1. AWS services (like EC2, RDS, Lambda) send metrics to CloudWatch
2. You create dashboards to visualize them
3. You set alarms to alert you when something goes wrong

**✅ Example:** You set a CloudWatch Alarm: "If CPU usage on EC2 > 80% for 5 minutes → send me an alert (email/SMS)."

### 💬 Common Interview Q&A for CloudWatch

#### Q1. What is Amazon CloudWatch?
**👉** It's a monitoring and observability service for AWS resources and apps.

#### Q2. What are CloudWatch Metrics?
**👉** Metrics are data points (like CPUUtilization, DiskReadOps) that show performance.

#### Q3. What is a CloudWatch Alarm?
**👉** An alarm watches a metric and performs actions when thresholds are crossed (e.g., send SNS notification or trigger Auto Scaling).

#### Q4. What is CloudWatch Logs?
**👉** Stores and monitors your application or system logs (like EC2 system logs).

#### Q5. What is the difference between CloudWatch and CloudTrail?

| Feature | CloudWatch | CloudTrail |
|---------|------------|------------|
| **Purpose** | Monitors performance | Tracks API calls (who did what) |
| **Data** | Metrics & Logs | Event history |
| **Example** | CPU usage 90% | User deleted an EC2 instance |

## ⚙️ Auto Scaling (EC2 Auto Scaling)

### 🧠 What is Auto Scaling?

Auto Scaling automatically adds or removes EC2 instances based on traffic or performance.

Think of it like this: "If traffic increases → launch more servers. If traffic decreases → shut down unused servers."

This saves cost 💰 and ensures high availability 🚀.

### ⚙️ How It Works

1. You define an **Auto Scaling Group (ASG)**
2. You set:
   - Minimum instances (always running)
   - Maximum instances (limit for scaling)
   - Desired capacity (normal number of instances)
3. You link CloudWatch Alarms:
   - If CPU > 80% → scale out (add EC2s)
   - If CPU < 20% → scale in (remove EC2s)

**✅ Example:** A shopping site gets heavy traffic during sales. Auto Scaling adds 4 extra EC2 servers automatically — and removes them when traffic reduces.

### 💬 Common Interview Q&A for Auto Scaling

#### Q1. What is EC2 Auto Scaling?
**👉** It's a service that automatically adjusts the number of EC2 instances based on demand.

#### Q2. What are the components of Auto Scaling?
- **Launch Template/Configuration**: defines EC2 setup (AMI, instance type, etc.)
- **Auto Scaling Group (ASG)**: manages multiple EC2 instances
- **Scaling Policies**: rules to scale in/out automatically

#### Q3. What are the types of scaling policies?

| Type | Description |
|------|-------------|
| **Target Tracking** | Maintains a target metric (e.g., keep CPU at 50%). |
| **Simple Scaling** | Scales when a specific alarm triggers. |
| **Step Scaling** | Scales gradually based on alarm thresholds. |
| **Scheduled Scaling** | Scales at specific times (e.g., every morning). |

#### Q4. What is the benefit of Auto Scaling?
**👉** High availability + cost optimization. It keeps performance stable and saves money by not running unnecessary instances.

#### Q5. How does CloudWatch help Auto Scaling?
**👉** CloudWatch monitors metrics → triggers alarms → alarms activate Auto Scaling policies → AWS adds/removes instances automatically.

### 🧩 Simple Diagram (Conceptually)
