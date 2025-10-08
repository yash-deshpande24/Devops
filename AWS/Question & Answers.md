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

# AWS IAM (Identity and Access Management) & Amazon EFS (Elastic File System) — Interview Q&A

---

## 🔐 AWS IAM (Identity and Access Management)

### 1. What is IAM?

**IAM** is a security service that helps you control who can access your AWS resources and what they can do.

> In simple words:  
IAM is like the security guard of AWS — it decides who can enter (users) and what they can do (permissions).

**Example:**  
Imagine you have a company AWS account:
- You want the developer to manage EC2.
- The finance team should only view billing.
- The admin should manage everything.

IAM lets you create users, assign permissions, and apply security rules to do exactly that.

---

### 2. Key Components of IAM

| Component    | Description                       | Example                        |
|--------------|-----------------------------------|--------------------------------|
| Users        | Individual accounts to access AWS | “yash_dev”, “finance_user”     |
| Groups       | Collection of users with same permissions | “Developers”, “Admins”         |
| Roles        | Temporary access to AWS services  | EC2 assumes a role to access S3|
| Policies     | JSON documents that define permissions | Allow EC2 to read from S3      |
| Access Keys  | Used for programmatic access via CLI or SDK | Used by scripts or apps        |

---

### 3. Example Policy (in simple form)

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
> This policy allows the user full access to all S3 buckets.

---

### 4. IAM Features

- ✅ Granular permissions – You can control actions down to the resource level.
- ✅ Free service – IAM itself has no cost.
- ✅ Global – IAM is not region-specific.
- ✅ Secure access – Uses MFA (Multi-Factor Authentication).
- ✅ Integration – Works with all AWS services.

---

### 5. Real-World Example

You create:
- **User:** dev_john
- **Group:** Developers
- **Policy:** Allow access to EC2 and S3 only
- **Attach policy to group**

Now, John can use EC2 and S3 but cannot delete IAM users or view billing.

---

### 6. Common Interview Questions & Answers

**Q1. What is IAM in AWS?**  
👉 IAM is a web service that helps you securely control access to AWS resources by defining who can access what.

**Q2. What are IAM Users?**  
👉 IAM users are individual identities with long-term credentials to access AWS services.

**Q3. What is the difference between IAM User and IAM Role?**

| Feature      | IAM User            | IAM Role                       |
|--------------|---------------------|--------------------------------|
| Access Type  | Long-term credentials| Temporary credentials         |
| Used By      | Humans              | AWS services or applications   |
| Example      | Developer logging in| EC2 instance accessing S3      |

**Q4. What is an IAM Policy?**  
👉 A JSON document that defines permissions — it tells what actions are allowed or denied.  
Example: “Allow S3 Read and Write” or “Deny EC2 Termination”.

**Q5. What are IAM Groups?**  
👉 A group of users that share the same permissions.  
E.g., All developers can launch EC2 instances.

**Q6. What is IAM Role used for?**  
👉 Roles are used when AWS services need to access other AWS services.  
Example:
- EC2 role that allows access to S3 bucket
- Lambda role that allows writing to DynamoDB

**Q7. What is MFA (Multi-Factor Authentication)?**  
👉 MFA adds an extra layer of security by requiring a password + a code from your phone or device to log in.

**Q8. What are the types of IAM policies?**

| Type                 | Description                     |
|----------------------|---------------------------------|
| AWS Managed Policy   | Created and managed by AWS      |
| Customer Managed Policy | Created and managed by you      |
| Inline Policy        | Directly attached to a single user, group, or role |

**Q9. What is the IAM Root User?**  
👉 The root user is the account created when you first sign up for AWS.  
It has full access to everything.  
⚠️ Should not be used daily — create IAM users instead.

**Q10. What are IAM Access Keys?**  
👉 Used for programmatic access (via AWS CLI or SDK).  
They include:
- Access Key ID
- Secret Access Key

**Q11. How do you secure IAM? (Best Practices)**
- ✅ Enable MFA for all users
- ✅ Use roles instead of embedding access keys in code
- ✅ Grant least privilege (only what’s necessary)
- ✅ Rotate access keys regularly
- ✅ Never share credentials

**Q12. What are Service-Linked Roles?**  
👉 These are IAM roles predefined by AWS and linked directly to a specific AWS service.  
Example: AWSServiceRoleForAutoScaling.

**Q13. Can IAM be used across all regions?**  
👉 Yes ✅ IAM is a global service — it is not tied to a specific region.

**Q14. How to give temporary access to a user?**  
👉 Use IAM Roles + STS (Security Token Service) to generate temporary credentials.

**Q15. What is the difference between IAM and AWS Organizations?**

| Feature      | IAM                     | AWS Organizations                 |
|--------------|-------------------------|-----------------------------------|
| Purpose      | Manage permissions in one account | Manage multiple AWS accounts      |
| Scope        | Single AWS account      | Multiple AWS accounts             |
| Example      | Create users and roles  | Central billing and consolidated policies |

---

### 7. Real-World Scenario Question

**Q: You have a developer who needs access to only one S3 bucket — how will you set it up?**  
**A:**  
- Create an IAM user → developer_user
- Create a custom policy allowing access to that specific bucket:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": ["arn:aws:s3:::my-bucket", "arn:aws:s3:::my-bucket/*"]
    }
  ]
}
```

- Attach this policy to the user.

---

### 1. IAM User vs Role vs Policy — Simplified Explanation

| Concept | Purpose           | Used By                    | Credentials            | Example                        |
|---------|-------------------|----------------------------|------------------------|--------------------------------|
| User    | Represents a person who logs in to AWS | Humans (developers, admins) | Long-term (username/password, access key) | “Yash” logs in to AWS console  |
| Role    | Provides temporary permissions to access AWS services | AWS services or external users | Temporary credentials (no password) | EC2 role that allows S3 access |
| Policy  | A rulebook that defines what actions are allowed or denied | Attached to users, roles, or groups | N/A                   | “Allow EC2:StartInstances”     |

**Easy Analogy:**  
Think of your AWS account like an office:

- User → Employee with their own ID card 🧍‍♂️
- Role → Visitor pass 🪪 (temporary access for specific tasks)
- Policy → Rulebook 📜 that says what you can or can’t do in the office

**Example Scenario:**  
Let’s say you have an EC2 instance that needs to access an S3 bucket.  
You don’t want to store access keys inside the code.  
✅ Solution:
- Create an IAM Role with S3 read-only policy.
- Attach the role to the EC2 instance.
- Now EC2 can access S3 — securely and automatically — without any hardcoded credentials.

---

### 2. Detailed Questions & Answers

**Q1. What is an IAM User in AWS?**  
👉 An IAM User represents an individual identity in AWS with long-term credentials (password or access keys).  
Users can log into the AWS Management Console or access services via CLI.

**Q2. What is an IAM Role in AWS?**  
👉 A Role provides temporary permissions to access AWS resources.  
It doesn’t have a username or password.  
Used by:
- AWS services (like EC2, Lambda)
- Federated users (e.g., Google, Active Directory users)

**Q3. What is an IAM Policy?**  
👉 A Policy is a JSON document that defines what actions are allowed or denied on which resources.  
Example:
```json
{
  "Effect": "Allow",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-bucket/*"
}
```

**Q4. Can a user have multiple policies?**  
👉 Yes ✅  
A user can have multiple policies attached directly or indirectly through groups.

**Q5. Can multiple users share one role?**  
👉 Yes ✅  
Multiple users or AWS services can assume the same role to get temporary permissions.

**Q6. Can a role be assigned to a user?**  
👉 Not directly.  
But a user can assume a role temporarily (e.g., cross-account access or elevated privileges).

**Q7. What are the types of IAM policies?**

| Type            | Description        | Example                  |
|-----------------|-------------------|--------------------------|
| AWS Managed     | Predefined by AWS | AmazonS3FullAccess       |
| Customer Managed| Created by you    | Custom EC2 access policy |
| Inline          | Attached directly to one user/role/group | Special admin-only rule |

**Q8. What is the difference between Inline Policy and Managed Policy?**

| Feature     | Inline Policy      | Managed Policy     |
|-------------|-------------------|--------------------|
| Attached To | One specific user/group/role | Multiple entities |
| Reusability | No                | Yes                |
| Best For    | One-off permissions | Common/shared permissions |

**Q9. What is the IAM Root User?**  
👉 The root user is the first account created when you sign up for AWS — has full control over all resources.  
⚠️ Use it only for account setup and billing — not daily work.

**Q10. What is the difference between Identity-Based and Resource-Based Policies?**

| Type           | Attached To            | Example                              |
|----------------|-----------------------|--------------------------------------|
| Identity-Based | User, Group, or Role  | “Allow EC2:*” for user               |
| Resource-Based | Resource itself (e.g., S3 bucket) | S3 bucket allows access from a specific account |

**Q11. What is AssumeRole in IAM?**  
👉 It’s the process where an entity (user/service) temporarily takes the permissions of another role.  
Example:  
A developer in Account A assumes a role in Account B to access its resources.

**Q12. How does IAM Role work with EC2?**  
👉
- Create a role with an S3 access policy.
- Attach the role to an EC2 instance.
- Application on EC2 automatically gets temporary credentials to access S3 securely.

**Q13. Can you attach multiple roles to one EC2 instance?**  
👉 No ❌  
Each EC2 instance can only have one IAM role attached at a time.

**Q14. What is a Service-Linked Role?**  
👉 A special role that AWS automatically creates and manages for specific services (like Auto Scaling, ECS, etc.)  
Example: AWSServiceRoleForAutoScaling.

**Q15. What is STS (Security Token Service)?**  
👉 STS provides temporary security credentials (Access Key, Secret, Token) for IAM roles or federated users.

**Q16. What is the Least Privilege Principle?**  
👉 Always grant only the minimum permissions needed for a task.  
Example:  
If a user only needs to read S3, don’t give full S3 access.

**Q17. What’s the difference between Group and Role?**

| Feature      | IAM Group             | IAM Role                   |
|--------------|----------------------|----------------------------|
| Purpose      | Combine multiple users| Grant temporary permissions|
| Members      | Users only            | No members, only assumed   |
| Credentials  | Long-term             | Temporary                  |

**Q18. What are IAM Permission Boundaries?**  
👉 They set the maximum permissions a user or role can have — even if policies give more access.  
Example:  
A user policy allows EC2 full access, but boundary limits it to only StartInstances.

**Q19. How can you secure IAM best practices?**
- ✅ Use MFA
- ✅ Don’t share accounts
- ✅ Rotate access keys
- ✅ Apply least privilege
- ✅ Monitor with CloudTrail

**Q20. Scenario-Based Question**  
**Q: You want an EC2 instance to read files from S3 without storing keys in code. How would you do it?**  
**A:**
- Create an IAM Role with S3 read-only policy.
- Attach the role to the EC2 instance.
- EC2 will automatically assume that role and access S3 securely.

---

### Quick Summary Table

| Concept | Description                        | Example                          |
|---------|------------------------------------|----------------------------------|
| User    | Long-term identity for human access| Developer with AWS Console login |
| Role    | Temporary access for services      | EC2 accessing S3                 |
| Policy  | Permission document (JSON)         | “Allow S3:ListBucket”            |
| Group   | Collection of users                | “Developers” group               |

---

## 📁 Amazon EFS (Elastic File System)

### 1. What is EFS?

**EFS** (Elastic File System) is a fully managed, scalable file storage service for Linux-based applications that you can attach to multiple EC2 instances at the same time.

> In simple words:  
EFS is like a shared network drive that all your EC2 instances can use together.

---

### 2. How it Works

- You create an EFS file system in AWS.
- You mount it (connect it) to one or more EC2 instances (like attaching a USB drive).
- Files stored in EFS are accessible from all attached EC2s — at the same time.
- AWS automatically handles scaling, storage growth, and high availability.

---

### 3. Simple Example

Let’s say you have 3 EC2 web servers running a website.  
They all need to:
- Read/write the same images and logs
- Share the same files

✅ Instead of storing files separately on each EC2 (EBS),  
you use EFS → all EC2 instances access the same shared folder.

---

### 4. EFS vs EBS vs S3

| Feature      | EFS          | EBS             | S3                |
|--------------|--------------|-----------------|-------------------|
| Type         | File storage | Block storage   | Object storage    |
| Access       | Many EC2s at once | Only one EC2 at a time | Via API/HTTP      |
| Scalability  | Automatically scales | Fixed size    | Unlimited         |
| Performance  | High throughput | High IOPS      | Depends on access |
| Use Case     | Shared files for multiple servers | OS or app disk | Backup, static files |

---

### 5. EFS Architecture (Conceptually)

```
+--------------------------------------------+
|           Amazon Elastic File System       |
|  (Shared Storage Across Multiple AZs)      |
+--------------------------------------------+
          ↑             ↑            ↑
      EC2 #1         EC2 #2       EC2 #3
   (All share same files)
```

---

### 6. Common Interview Questions & Answers

**Q1. What is Amazon EFS?**  
👉 EFS is a fully managed network file system that allows multiple EC2 instances to access the same data concurrently.

**Q2. What type of storage is EFS?**  
👉 File-based storage (like a shared folder or NAS).

**Q3. What is the difference between EFS and EBS?**

| Feature     | EFS                  | EBS                     |
|-------------|----------------------|-------------------------|
| Access      | Many EC2s at once    | One EC2 at a time       |
| Type        | File system          | Block storage           |
| Scalability | Auto-scale           | Fixed size              |
| Use Case    | Shared app data      | OS/application disk     |

**Q4. What are the performance modes of EFS?**  
👉 EFS supports two performance modes:
- General Purpose – Low latency (for most workloads)
- Max I/O – Higher throughput, for parallel workloads (e.g., big data)

**Q5. What are the throughput modes in EFS?**
- Bursting – Default mode, auto scales with storage size
- Provisioned – You set the throughput manually

**Q6. Is EFS automatically scalable?**  
👉 Yes ✅  
EFS automatically grows and shrinks as you add or remove files — no manual resizing needed.

**Q7. Can EFS be accessed from multiple Availability Zones (AZs)?**  
👉 Yes ✅  
EFS is multi-AZ — it stores data redundantly across multiple AZs for high availability.

**Q8. How do you mount EFS on an EC2 instance?**  
👉 You use the NFS (Network File System) protocol.  
Example (Linux command):

```bash
sudo mount -t nfs4 -o nfsvers=4.1 fs-12345678.efs.ap-south-1.amazonaws.com:/ /mnt/efs
```

**Q9. Does EFS support Windows EC2 instances?**  
👉 ❌ No, EFS supports Linux-based instances only.  
For Windows, AWS provides FSx for Windows File Server.

**Q10. What are the storage classes in EFS?**
- EFS Standard – Frequently accessed data
- EFS Infrequent Access (IA) – Lower cost for rarely accessed data

EFS automatically moves files between them using Lifecycle Management.

**Q11. What is EFS Lifecycle Management?**  
👉 It automatically moves files that haven’t been accessed for a set period (e.g., 30 days) from Standard → IA (Infrequent Access) to save cost.

**Q12. What are EFS Mount Targets?**  
👉 Mount targets are network endpoints in each AZ that EC2 instances use to connect to EFS.  
Each subnet in your VPC needs a mount target for access.

**Q13. Is EFS regional or zonal?**  
👉 Regional ✅  
It stores data across multiple AZs in the same region for high durability.

**Q14. How is EFS billed?**
- Amount of data stored (GB per month)
- Data transfer out of AWS region
- Storage class (Standard or IA)

**Q15. How secure is EFS?**
- Supports IAM policies
- VPC security groups control network access
- Encryption in transit (TLS) and at rest

**Q16. What are the use cases of EFS?**
- ✅ Content management systems (WordPress, Drupal)
- ✅ Shared home directories for users
- ✅ Big data analytics
- ✅ Media processing
- ✅ Application logs shared between servers

**Q17. What is the difference between EFS Standard and EFS One Zone?**

| Feature        | EFS Standard | EFS One Zone           |
|----------------|--------------|------------------------|
| Availability   | Multi-AZ     | Single AZ              |
| Cost           | Higher       | Lower                  |
| Durability     | Higher       | Slightly lower         |
| Use Case       | Critical workloads | Backup or dev/test environments |

**Q18. Can EFS automatically back up data?**  
👉 Yes ✅ using AWS Backup, you can schedule automatic EFS backups.

**Q19. Can EFS be accessed by ECS or Lambda?**  
👉 Yes ✅  
- ECS tasks can mount EFS for shared storage.
- AWS Lambda can use EFS for storing large datasets.

**Q20. Is EFS Serverless?**  
👉 Partially ✅  
You don’t manage servers or storage — AWS handles scaling and availability — but you still mount it using EC2 or services like ECS or Lambda.

---

## Amazon EFS — Advanced & Scenario-Based Q&A

**Q21. What happens if one EC2 instance deletes a file from EFS?**  
👉 Since EFS is a shared file system, if one EC2 deletes a file, it is deleted for all instances that are connected — just like deleting a file from a shared Google Drive folder.

**Q22. Can EFS be used across multiple AWS regions?**  
👉 ❌ No.  
EFS is regional, meaning it can be accessed from multiple Availability Zones within the same region, but not across regions directly.  
You can, however, copy data using DataSync between regions.

**Q23. What is AWS DataSync in the context of EFS?**  
👉 AWS DataSync is a service used to move large amounts of data between on-premises storage, S3, and EFS quickly and securely.

**Q24. Can we use EFS in a private subnet?**  
👉 ✅ Yes.  
You can create EFS mount targets inside private subnets — just ensure your EC2 instances have network access (NFS port 2049) to it.

**Q25. What port does EFS use for communication?**  
👉 EFS uses TCP port 2049 for NFS (Network File System) connections.

**Q26. Can we access EFS from on-premises servers?**  
👉 ✅ Yes.  
If you use AWS Direct Connect or AWS VPN, on-premises servers can mount the EFS file system securely using NFS protocol.

**Q27. What is the durability and availability of EFS?**
- Durability: 99.999999999% (11 nines)
- Availability: 99.99% (multi-AZ setup)

AWS stores multiple copies of your data across multiple Availability Zones.

**Q28. Does EFS support encryption?**  
👉 ✅ Yes, EFS supports:
- Encryption at rest (via KMS)
- Encryption in transit (via TLS)

**Q29. What is the difference between EFS IA (Infrequent Access) and S3 Glacier?**

| Feature         | EFS IA     | S3 Glacier            |
|-----------------|------------|-----------------------|
| Access Type     | File System| Object Storage        |
| Access Speed    | Milliseconds| Minutes to hours     |
| Use Case        | Rarely accessed files in EFS | Long-term archive backups |

**Q30. How is performance scaled in EFS?**  
👉 EFS automatically scales performance as your data grows — both throughput and IOPS increase with size.  
You can also choose Provisioned Throughput for consistent high performance.

**Q31. What is the maximum size limit of EFS?**  
👉 There’s no limit.  
EFS grows and shrinks automatically as you add or remove files (petabyte-scale).

**Q32. What are the consistency models in EFS?**  
👉 EFS provides strong consistency — meaning:
- Immediately after writing, all EC2s see the updated data.
- No delay between writes and reads.

**Q33. How do you back up EFS data automatically?**  
👉 You can enable backups using AWS Backup, which can schedule:
- Daily or weekly backups
- Retention and lifecycle policies

**Q34. Can EFS replace S3?**  
👉 ❌ No.  
EFS and S3 serve different purposes:
- EFS: shared file system for EC2 (mountable, POSIX-compliant)
- S3: object storage for web apps, backups, and static content

**Q35. Can EFS be used as a root filesystem for EC2?**  
👉 ❌ No.  
EFS cannot be used as a boot/root volume — use EBS for that.  
EFS is for shared data, not the operating system.

**Q36. What happens when you unmount EFS from EC2?**  
👉 Files remain safely stored in EFS.  
Unmounting only disconnects your EC2 instance; the data remains in AWS until deleted manually.

**Q37. What kind of workloads are not suitable for EFS?**  
👉 EFS is not ideal for:
- High IOPS, low-latency database workloads (use EBS instead)
- Windows applications (use FSx for Windows)

**Q38. What tools can monitor EFS performance?**  
👉 You can use:
- Amazon CloudWatch (for metrics like I/O, throughput)
- AWS CloudTrail (for API activity logs)

**Q39. What are some key metrics to monitor for EFS?**
- BurstCreditBalance
- PercentIOLimit
- DataReadIOBytes
- DataWriteIOBytes
- TotalIOBytes

**Q40. Can EFS be used with AWS Lambda?**  
👉 ✅ Yes.  
Lambda functions can mount EFS to access large files, shared datasets, or libraries during execution.

**Q41. What are EFS Access Points?**  
👉 Access Points are application-specific entry points into an EFS file system.  
They simplify access permissions and make it easier to manage multiple users or apps securely.

Example:
- /home/app1 for App 1
- /home/app2 for App 2

**Q42. Can I limit access to specific users or instances in EFS?**  
👉 ✅ Yes.  
You can use:
- IAM policies
- Security groups
- Access Points

to control which users or EC2 instances can access EFS.

**Q43. What is the latency of EFS compared to EBS?**  
👉 EFS has slightly higher latency than EBS since it’s a network file system.  
EBS is directly attached to the EC2 instance and hence faster.

**Q44. Can I use EFS in multiple VPCs?**  
👉 ✅ Yes, using VPC peering or Transit Gateway, you can share EFS between different VPCs in the same region.

**Q45. What are the data transfer costs in EFS?**
- Within the same region: free
- Across regions or VPCs: data transfer costs apply
- To/from EC2 instances: charged based on the EC2-to-EFS network traffic if across AZs

**Q46. How does EFS handle failure in one AZ?**  
👉 If one Availability Zone fails, data is still available from other AZs — thanks to multi-AZ replication.

**Q47. Is EFS serverless?**  
👉 Partially.  
You don’t manage servers or storage provisioning, but it still requires clients (like EC2, Lambda) to mount and access it.

**Q48. What permissions are required to mount EFS?**
- EC2 instances must:
  - Have NFS port (2049) open in their security group
  - Have network access to the EFS mount target
  - Have IAM role permissions if using Access Points

**Q49. What command is used to mount EFS manually in Linux?**  
👉 Example:

```bash
sudo mount -t nfs4 -o nfsvers=4.1 fs-12345678.efs.us-east-1.amazonaws.com:/ /mnt/efs
```

**Q50. What are some real-world use cases of EFS?**
- ✅ Shared web content for multiple EC2s (like WordPress)
- ✅ Centralized log storage
- ✅ Big data analytics pipelines
- ✅ Shared libraries for AWS Lambda
- ✅ Container workloads in ECS or EKS

---
