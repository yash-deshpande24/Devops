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


CloudWatch checks CPU → triggers Auto Scaling → adjusts EC2 count.

## 🔍 Advanced EC2 Questions

### Q1. What is the difference between EC2 and a physical server?
**👉** EC2 is a virtual machine that runs in AWS's data centers, while a physical server is your own hardware. In EC2, AWS manages the hardware — you only manage the software.

### Q2. What is an EBS Volume?
**👉** EBS (Elastic Block Store) is storage for EC2 instances — like a hard disk. When you launch an EC2, it uses EBS to store data (OS, files, etc.). You can detach, attach, or back it up easily.

### Q3. What are the EC2 instance states?
**👉**
- **Pending** → being launched
- **Running** → currently active
- **Stopped** → powered off, can be restarted
- **Terminated** → permanently deleted

### Q4. What is the difference between an Elastic IP and a Public IP?
**👉**
- **Public IP** changes every time you stop/start an instance
- **Elastic IP** stays the same even after reboot (static)

### Q5. What are EC2 Placement Groups?
**👉** Used to control how instances are placed on AWS hardware:
- **Cluster** → high-performance computing (low latency)
- **Spread** → separate hardware (for high availability)
- **Partition** → for big data apps (isolates partitions)

### Q6. What are EC2 Spot Instances used for?
**👉** Spot Instances are cheap unused EC2 capacity — great for:
- Batch jobs
- Data analysis
- Non-critical workloads

⚠️ AWS can stop them anytime if demand increases.

### Q7. What is an EC2 Launch Template?
**👉** A template that saves EC2 settings (AMI, instance type, key pair, etc.) so you can launch new instances or Auto Scaling groups easily.

### Q8. How can you connect to an EC2 instance?
**👉**
- **Linux EC2**: via SSH using .pem key
- **Windows EC2**: via RDP using password or key

## 🔍 Advanced CloudWatch Questions

### Q1. What types of data can CloudWatch monitor?
**👉** It monitors:
- Metrics (CPU, memory, disk, etc.)
- Logs (system or app logs)
- Events (AWS resource changes)
- Alarms (notifications or triggers)

### Q2. What are Custom Metrics in CloudWatch?
**👉** Metrics you send from your own application.

**Example:** `PutMetricData API → sends "NumberOfActiveUsers" = 150`

### Q3. What are CloudWatch Dashboards?
**👉** A visual view (graphs and charts) to monitor your AWS resources in one place — you can combine CPU, RAM, and network graphs on a single screen.

### Q4. What are CloudWatch Events (or EventBridge)?
**👉** They react to changes in your AWS resources.

**Example:** When an EC2 instance stops → automatically send an email or start another instance.

### Q5. How long does CloudWatch store data?
**👉**
- 1-minute data points → stored for 15 days
- 5-minute & 1-hour data → stored for 63 days (2 months)
- Older (aggregated) data → stored for 15 months

### Q6. Can CloudWatch monitor on-premise servers?
**👉** Yes ✅ — you can install the CloudWatch Agent on your local servers to push metrics and logs to CloudWatch.

## 🔍 Advanced Auto Scaling Questions

### Q1. What is an Auto Scaling Group (ASG)?
**👉** A logical group of EC2 instances that are managed together for scaling and availability.

### Q2. What are scaling policies?
**👉** Rules that define when and how to add or remove instances:
- **Target Tracking** → keeps metric (like CPU) at target
- **Step Scaling** → scales gradually
- **Simple Scaling** → scales when a single alarm triggers
- **Scheduled Scaling** → scales at fixed times

### Q3. What is a Launch Configuration / Template in Auto Scaling?
**👉** It defines how new instances will look — OS, instance type, security groups, key pair, etc.

💡 **Launch Template** = newer version (recommended).

### Q4. What happens if an instance in an Auto Scaling group fails?
**👉** Auto Scaling automatically replaces unhealthy instances to maintain the desired count.

### Q5. Can you use Auto Scaling without CloudWatch?
**👉** Not really. CloudWatch metrics (like CPU usage) are used as triggers for scaling actions.

### Q6. What are Lifecycle Hooks in Auto Scaling?
**👉** They pause the instance during scaling (launch or terminate) so you can perform custom actions — like running a setup script or backup before it's deleted.

### Q7. What's the difference between Vertical and Horizontal Scaling?

| Type | Description | Example |
|------|-------------|---------|
| **Vertical** | Increase resources (CPU/RAM) of one server | t2.micro → t2.large |
| **Horizontal** | Add more servers | Add 2 EC2s when traffic increases |

Auto Scaling performs **Horizontal Scaling**.

### Q8. How does Auto Scaling improve fault tolerance?
**👉** If one instance fails, Auto Scaling automatically launches another to maintain performance and uptime.

---

## AWS IAM (Identity and Access Management)

### 1. What is IAM?
IAM is a security service that helps you control who can access your AWS resources and what they can do.

*In simple words:*

IAM is like the security guard of AWS — it decides who can enter (users) and what they can do (permissions).

### Example:
Imagine you have a company AWS account:
- Developer manages EC2
- Finance team views billing only
- Admin manages everything

IAM lets you create users, assign permissions, and apply security rules to do exactly that.

### 2. Key Components of IAM
| Component | Description | Example |
| --------- | ----------- | ------- |
| Users     | Individual accounts to access AWS | “yash_dev”, “finance_user” |
| Groups    | Collection of users with same permissions | “Developers”, “Admins” |
| Roles     | Temporary access to AWS services | EC2 assumes a role to access S3 |
| Policies  | JSON documents that define permissions | Allow EC2 to read from S3 |
| Access Keys | Used for programmatic access via CLI or SDK | Used by scripts or apps |

### 3. Example Policy (Simple)
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "*"
    }
  ]
}
```
This policy allows the user full access to all S3 buckets.

### 4. IAM Features
- Granular permissions – control actions down to the resource level.
- Free service – no cost.
- Global – not region-specific.
- Secure access – uses MFA (Multi-Factor Authentication).
- Integration – works with all AWS services.

### 5. Real-World Example
- User: dev_john
- Group: Developers
- Policy: Allow access to EC2 and S3 only
- Attach policy to group
John can use EC2 and S3 but cannot delete IAM users or view billing.

### 6. Common Interview Questions & Answers
- **Q1: What is IAM in AWS?**
  - A web service to securely control access to AWS resources.
- **Q2: What are IAM Users?**
  - Individual identities with long-term credentials.
- **Q3: Difference between IAM User and IAM Role:**
  | Feature | IAM User | IAM Role |
  |---------|----------|----------|
  | Access Type | Long-term credentials | Temporary credentials |
  | Used By | Humans | AWS services or applications |
  | Example | Developer logging in | EC2 instance accessing S3 |
- **Q4: What is an IAM Policy?**
  - JSON document defining permissions.
- **Q5: What are IAM Groups?**
  - Groups of users with shared permissions.
- **Q6: What is IAM Role used for?**
  - AWS services needing access to other services.
- **Q7: What is MFA?**
  - Extra security requiring password + device code.
- **Q8: Types of IAM policies:**
  | Type | Description |
  |-------|-------------|
  | AWS Managed Policy | Created/managed by AWS |
  | Customer Managed Policy | Created/managed by you |
  | Inline Policy | Directly attached to single user/group/role |
- **Q9: What is the IAM Root User?**
  - Original account with full access, use sparingly.
- **Q10: What are IAM Access Keys?**
  - Programmatic access credentials.
- **Q11: Best practices to secure IAM:**
  - Enable MFA, least privilege principle, rotate keys, don’t share credentials.

---

## Amazon EFS (Elastic File System)

### 1. What is EFS?
EFS is a fully managed, scalable file storage for Linux-based apps, attachable to multiple EC2 instances.

*In simple words:*

EFS is a shared network drive all your EC2s can use simultaneously.

### 2. How it Works
- Create EFS file system
- Mount it to EC2 instances
- Files are accessible simultaneously
- AWS handles scaling, storage growth, and availability

### 3. Simple Example
Three EC2 web servers share the same images and logs using EFS instead of separate EBS volumes.

### 4. EFS vs EBS vs S3
| Feature | EFS | EBS | S3 |
|---------|-----|-----|----|
| Type | File storage | Block storage | Object storage |
| Access | Many EC2s | One EC2 only | API/HTTP |
| Scalability | Auto scales | Fixed size | Unlimited |
| Performance | High throughput | High IOPS | Depends on access |
| Use Case | Shared files across servers | OS or app disk | Backup/static files |

### 5. EFS Architecture
```
Amazon Elastic File System (Shared Storage Across AZs)
         ↑        ↑        ↑
      EC2 #1    EC2 #2    EC2 #3
     (All share same files)
```

### 6. Common Interview Questions & Answers
- **Q1: What is Amazon EFS?**
  - A managed network file system for concurrent multiple EC2 access.
- **Q2: Difference between EFS and EBS:**
  | Feature | EFS | EBS |
  |---------|-----|-----|
  | Access | Many EC2s | One EC2 at a time |
  | Type | File system | Block storage |
  | Scalability | Auto-scale | Fixed size |
  | Use Case | Shared app data | OS/app disk |
- **Q3: Performance modes:** General Purpose (low latency), Max I/O (high throughput)
- **Q4: Throughput modes:** Bursting (auto), Provisioned (manual)
- **Q5: Is EFS scalable?** Yes
- **Q6: Multi-AZ accessible?** Yes
- **Q7: Mount with NFS:** `sudo mount -t nfs4 -o nfsvers=4.1 fs-xxxx.efs.region.amazonaws.com:/ /mnt/efs`
- **Q8: Supports Windows?** No
- **Q9: Storage classes:** Standard and Infrequent Access (IA)
- **Q10: Lifecycle Management:** Moves files between classes to save cost
- **Q11: Mount targets:** Network endpoints per AZ
- **Q12: Regional service?** Yes
- **Q13: Billing:** Data stored, transfer, class
- **Q14: Security:** IAM, encryption, security groups
- **Q15: Use cases:** CMS, logs, analytics, media, shared apps
