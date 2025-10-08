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
**👉** On-Demand**: Pay per hour or second — no long-term contract.
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

## 🌐 AWS VPC (Virtual Private Cloud)

### 1. What is VPC?
A VPC is a virtual network in AWS where you can launch AWS resources (EC2, RDS, Lambda, etc.).

- **Simple analogy**: Your own private data center in the cloud, where you control IPs, subnets, routing, and security.

#### Example
- VPC with:
  - 2 subnets: public (web servers), private (databases)
  - EC2 instances in both subnets
  - Internet access only for public subnet

Resources are securely isolated but can be reachable if needed.

---

### 2. Key Components of VPC

| Component         | Description                         | Example                               |
|-------------------|-------------------------------------|---------------------------------------|
| Subnet            | Divides VPC into smaller networks   | Public subnet, Private subnet         |
| Route Table       | Controls traffic flow               | 0.0.0.0/0 → Internet Gateway          |
| Internet Gateway  | Provides internet access            | For public EC2s                       |
| NAT Gateway       | Private subnet EC2s → internet      | For OS updates                        |
| Security Group    | Virtual firewall for instances      | Allow port 22 (SSH)                   |
| Network ACL       | Firewall for subnets                | Deny traffic from certain IPs         |
| Elastic IP        | Static public IP                    | For EC2 in public subnet              |

---

### 3. VPC Types
- **Default VPC**: Created automatically in each region, easy for beginners.
- **Custom VPC**: User-defined IP range, subnets, route tables, etc.

---

### 4. Public vs Private Subnet

| Feature         | Public Subnet        | Private Subnet         |
|-----------------|---------------------|------------------------|
| Internet Access | Yes                 | No                     |
| Examples        | Web servers         | Databases              |
| How             | Internet Gateway    | NAT Gateway outbound   |

---

### 5. VPC Diagram (Conceptual)

```
         Internet
             |
         Internet Gateway
             |
      +----------------+
      |     VPC        |
      +----------------+
    /                    \
Public Subnet         Private Subnet
(Web servers)         (Database/App)
```

---

### 6. Common Interview Q&A

#### Q1. What is an AWS VPC?
A logically isolated section of AWS to launch resources in a private network.

#### Q2. What is the default VPC?
Automatically created in each region, public subnet in each AZ, EC2s get public IP by default.

#### Q3. VPC vs Subnet?
- VPC: Entire virtual network
- Subnet: Subdivision of VPC

#### Q4. What is an Internet Gateway?
IGW connects VPC to the Internet; public subnet EC2s use it.

#### Q5. What is a NAT Gateway?
Allows private subnet EC2s outbound internet (updates), not inbound.

#### Q6. What is a Route Table?
Defines where traffic goes (e.g. 0.0.0.0/0 → IGW).

#### Q7. Security Groups vs Network ACLs

| Feature         | Security Group      | Network ACL           |
|-----------------|--------------------|-----------------------|
| Level           | Instance-level      | Subnet-level          |
| Type            | Stateful            | Stateless             |
| Default         | Deny all inbound    | Allow all in/out      |
| Rules           | Allow needed ports  | Explicit allow/deny   |

#### Q8. What is VPC Peering?
Connect two VPCs for private IP communication (same/different account), no transitive routing.

#### Q9. VPC to On-premises?
Yes: AWS VPN (IPSec) or Direct Connect.

#### Q10. What is Elastic IP?
Static public IP assignable to EC2.

#### Q11. What is VPC Endpoint?
Private connection to AWS services (S3, DynamoDB) without internet.

#### Q12. What is CIDR in VPC?
Defines VPC IP range, e.g. 10.0.0.0/16.

#### Q13. Multi-AZ deployment in VPC?
Resources across multiple AZs for HA.

#### Q14. What is VPC Flow Logs?
Captures IP traffic for monitoring/troubleshooting.

#### Q15. Public vs Private IP in VPC?

| Type      | Access             | Use Case        |
|-----------|--------------------|-----------------|
| Public IP | Internet reachable | Web servers     |
| Private IP| Only in VPC        | Database servers|

#### Q16. NAT Instance vs NAT Gateway

| Feature      | NAT Instance      | NAT Gateway      |
|--------------|------------------|------------------|
| Managed      | User-managed     | AWS-managed      |
| Scaling      | Manual           | Automatic        |
| Availability | Single EC2       | Multi-AZ         |
| Performance  | Limited          | High throughput  |

#### Q17. IPv6 CIDR block in VPC?
Supports IPv6 (CIDR /56), can coexist with IPv4.

#### Q18. Overlapping CIDR blocks in peered VPCs?
No, overlapping CIDRs not allowed.

#### Q19. Bastion Host?
Jump server in public subnet to securely access private subnet instances.

#### Q20. Scenario: Web server (public), DB (private), DB not exposed to internet?
- Create VPC
- Public subnet: web EC2, IGW attached
- Private subnet: DB EC2, no IGW, security group allows access from web server
- Optional: NAT Gateway for private subnet EC2 internet access

---

## 🌐 AWS VPC — Advanced Questions & Answers

#### Q21. EC2 in one VPC communicate with another?
Yes: VPC Peering, Transit Gateway, or VPN.

#### Q22. Transit Gateway?
Connects multiple VPCs and on-prem networks, simplifies network management.

#### Q23. VPC Endpoint and Why?
Private access to AWS services without internet. Two types:
- Interface Endpoint (ENI)
- Gateway Endpoint (S3/DynamoDB)

#### Q24. Gateway Endpoint vs Interface Endpoint

| Feature      | Gateway Endpoint   | Interface Endpoint         |
|--------------|-------------------|---------------------------|
| Service      | S3, DynamoDB      | Most AWS services         |
| Type         | Gateway           | ENI                       |
| Cost         | Free              | Paid                      |
| Access       | Route Table       | Private IP                |

#### Q25. NAT Instance vs NAT Gateway (again)

| Feature      | NAT Instance     | NAT Gateway           |
|--------------|-----------------|-----------------------|
| Managed      | User-managed    | AWS-managed           |
| Availability | Single instance | Multi-AZ supported    |
| Scaling      | Manual          | Automatic             |
| Performance  | Limited         | High throughput       |
| Cost         | Cheaper         | More expensive        |

#### Q26. How to secure your VPC?
- Use Security Groups & NACLs
- Avoid public IPs for private resources
- Enable VPC Flow Logs
- Restrict with IAM and VPC endpoints

#### Q27. VPC Peering Limitations
- No overlapping CIDRs
- No transitive routing
- Max 125 peering connections (soft limit)

#### Q28. Multiple CIDR blocks in VPC?
Yes, supports secondary CIDR blocks.

#### Q29. Security Group vs NACL (again)

| Feature      | Security Group   | NACL                 |
|--------------|-----------------|----------------------|
| Type         | Stateful        | Stateless            |
| Level        | Instance        | Subnet               |
| Default      | Deny inbound    | Allow all in/out     |
| Use          | Protect instance| Protect subnet       |

#### Q30. Private subnet EC2s internet access?
Use NAT Gateway in public subnet, route private subnet’s 0.0.0.0/0 to NAT Gateway.

#### Q31. Bastion Host and why?
Jump server in public subnet for secure SSH/RDP into private subnet.

#### Q32. Public, Private, Isolated Subnets

| Subnet Type | Internet Access | Example                          |
|-------------|----------------|-----------------------------------|
| Public      | Yes            | Web servers                       |
| Private     | No             | Databases (use NAT for outbound)  |
| Isolated    | No             | Highly secure workloads           |

#### Q33. VPC Flow Log?
Captures network traffic for VPC/subnet/ENI; troubleshooting/security/compliance.

#### Q34. Typical VPC limits
- Default VPC/region: 1
- Subnets/VPC: 200
- IGWs/VPC: 1
- Security groups/VPC: 500
- NACLs/VPC: 200

#### Q35. Connect VPCs across AWS accounts?
Yes: VPC Peering or Transit Gateway.

#### Q36. Public vs Private IP in VPC (again)

| IP Type   | Accessibility      | Use Case    |
|-----------|--------------------|-------------|
| Public IP | Internet reachable | Web servers |
| Private IP| Inside VPC only    | Databases   |

#### Q37. EC2 access S3 privately?
Use VPC Gateway Endpoint for S3; update route table.

#### Q38. Multi-region VPC design?
Connect VPCs in different regions via VPN or Transit Gateway.

#### Q39. NAT Gateway vs IGW

| Feature       | NAT Gateway          | Internet Gateway (IGW)     |
|---------------|---------------------|----------------------------|
| Access Type   | Outbound only        | Inbound & Outbound         |
| Use Case      | Private subnet EC2s  | Public subnet EC2s         |
| Managed       | AWS-managed          | AWS-managed                |

#### Q40. Scenario: Web app, web server in public subnet, DB in private, users via HTTPS?
- VPC with public/private subnets in 2 AZs (HA)
- Public subnet: web server, IGW attached
- Private subnet: DB, no IGW, security group allows access from web server
- NAT Gateway in public subnet if DB needs updates
- Security Groups allow HTTPS to web server

---

# AWS S3 Interview FAQ

This file contains concise Q&A notes, tables, and scenario answers for Amazon S3.

---

## ☁️ Amazon S3 (Simple Storage Service)

### 1. What is Amazon S3?
S3 is a fully managed object storage service for any type of data: files, images, videos, backups, logs, etc.

- **Simple Analogy**: S3 = highly durable cloud hard drive, accessible from anywhere.

#### Example
Web app uploads user profile images to S3 instead of EC2. Users access images via S3 URL.

---

### 2. Key Concepts of S3

| Component        | Description                   | Example              |
|------------------|------------------------------|----------------------|
| Bucket           | Container for objects         | my-app-images        |
| Object           | Actual file stored in S3      | profile1.jpg         |
| Key              | Unique identifier for object  | images/profile1.jpg  |
| Versioning       | Track object versions         | Enable, restore old  |
| Storage Classes  | Cost/performance options      | Standard, Glacier    |
| Lifecycle Policy | Auto move/delete objects      | Move to Glacier 30d  |

---

### 3. S3 Storage Classes

| Storage Class           | Use Case                | Durability  | Cost     |
|-------------------------|-------------------------|-------------|----------|
| Standard                | Frequent access         | 11 9’s      | High     |
| Standard-IA             | Infrequent access       | 11 9’s      | Lower    |
| One Zone-IA             | Rare, single AZ         | 11 9’s      | Cheapest |
| Glacier                 | Archival                | 11 9’s      | Low      |
| Glacier Deep Archive    | Long-term backup        | 11 9’s      | Lowest   |

---

### 4. S3 Features

- High durability: 99.999999999% (11 nines)
- Scalable: Unlimited objects
- Secure: Encryption (at rest, in transit)
- Accessible: Console, CLI, SDK, REST API
- Versioning
- Event Notifications (trigger Lambda/SQS on upload/delete)

---

### 5. Common Interview Questions & Answers

#### Q1. What is Amazon S3?
Object storage for files, backups, logs, images, etc. Highly durable, scalable, secure.

#### Q2. What is a bucket?
Container for objects, globally unique name.

#### Q3. What is an object?
File stored: data + metadata + key (unique ID).

#### Q4. S3 object size limits?
- Max single object: 5 TB
- Max PUT upload: 5 GB
- Large files: Multipart upload

#### Q5. S3 storage classes?
Standard, Standard-IA, One Zone-IA, Glacier, Glacier Deep Archive

#### Q6. What is versioning?
Keeps multiple versions, restore deleted/overwritten files.

#### Q7. S3 lifecycle policy?
Auto-transition objects between classes or delete. Example: move logs to Glacier after 30 days.

#### Q8. S3 bucket policy?
JSON policy to control access.

```json
{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::my-bucket/*"
}
```

#### Q9. What is S3 ACL?
Access Control List for fine-grained permissions.

#### Q10. Bucket Policy vs ACL

| Feature   | Bucket Policy | ACL         |
|-----------|---------------|-------------|
| Scope     | Bucket/objects| Individual  |
| Control   | JSON-based    | Limited     |
| Flexible  | High          | Low         |

#### Q11. How to secure S3 data?
- Encryption at rest (SSE-S3, SSE-KMS)
- Encryption in transit (HTTPS)
- IAM & bucket policies
- MFA Delete
- Logging & monitoring

#### Q12. S3 Event Notification?
Trigger events (upload, delete, restore). Example: upload triggers Lambda to process image.

#### Q13. Multipart upload?
Upload large objects (>5 GB) in parts, reliable & faster.

#### Q14. S3 Transfer Acceleration?
Faster uploads/downloads via CloudFront edge locations.

#### Q15. S3 vs EBS

| Feature    | S3            | EBS                  |
|------------|---------------|----------------------|
| Type       | Object storage| Block storage        |
| Access     | HTTP API      | EC2 mount            |
| Use Case   | Files, backup | OS, databases        |
| Durability | 11 9’s        | 99.999%              |

#### Q16. S3 vs EFS

| Feature   | S3            | EFS                |
|-----------|---------------|--------------------|
| Type      | Object        | File               |
| Access    | HTTP/REST API | NFS mount          |
| Multi-Access | Yes (API)  | Yes (EC2 mount)    |
| Use Case  | Backup, logs  | Shared files EC2   |

#### Q17. S3 as static website?
Yes. Enable hosting, upload HTML/CSS/JS, access via endpoint or custom domain.

#### Q18. S3 Cross-Region Replication (CRR)?
Auto-replicates objects to bucket in another region.

#### Q19. S3 Object Lock?
Prevents object deletion/modification for retention (compliance).

#### Q20. Scenario: Cheap storage for old user files, recoverable?
- S3 Standard for active, Lifecycle Policy to Glacier after 30 days
- Enable versioning
- Bucket policy & encryption

---

## ☁️ Amazon S3 — Advanced Q&A

#### Q21. Max buckets per AWS account?
100 per region (default), limit can be increased.

#### Q22. S3 vs file system?
S3 = object store, not hierarchical. Access via API, not POSIX.

#### Q23. S3 limits?
- Object size: 0 bytes – 5 TB
- Max PUT: 5 GB
- Max objects: unlimited
- Max buckets: 100 (default)

#### Q24. Eventual Consistency?
New objects: read-after-write. Overwrite/delete: eventual consistency (may see older data briefly).

#### Q25. Strong Consistency?
AWS now provides strong read-after-write for all PUTs/DELETEs globally.

#### Q26. S3 Replication Time Control (RTC)?
Guarantees objects replicate within 15 minutes (mission-critical DR).

#### Q27. CRR vs SRR

| Feature   | CRR (Cross-Region) | SRR (Same-Region)    |
|-----------|--------------------|----------------------|
| Region    | Different          | Same                 |
| Use Case  | DR, geo-redundancy | Compliance, locality |
| Cost      | Higher             | Lower                |

#### Q28. Multipart Upload?
Break large files into parts, upload parallel, resume failed uploads.

#### Q29. Restrict access to IPs?
Bucket policy with Condition for IpAddress.

```json
"Condition": {
  "IpAddress": {"aws:SourceIp": "203.0.113.0/24"}
}
```

#### Q30. Glacier & Glacier Deep Archive?
- Glacier: archival, retrieval in minutes/hours
- Deep Archive: cheapest, retrieval in hours
- Use lifecycle rules to move data.

#### Q31. S3 Transfer Acceleration?
Speeds uploads/downloads over long distances via CloudFront.

#### Q32. Bucket Policy vs IAM Policy

| Feature | Bucket Policy | IAM Policy           |
|---------|--------------|----------------------|
| Scope   | Bucket-level | User/group/role      |
| Control | Bucket access| Permissions AWS-wide |

#### Q33. S3 Object Lock?
Prevents deletion/modification; governance and compliance modes.

#### Q34. S3 triggers Lambda?
Yes. Events: PUT, DELETE, POST, COPY.

#### Q35. S3 Select?
Retrieve specific data from objects (CSV, JSON), faster and less transfer.

#### Q36. S3 Object Metadata?
Describes object (size, type, date), plus custom metadata.

#### Q37. S3 Standard vs Standard-IA vs One Zone-IA

| Feature         | Standard | Standard-IA | One Zone-IA |
|-----------------|----------|-------------|-------------|
| Access freq     | Frequent | Infrequent  | Infrequent  |
| Availability    | 99.99%   | 99.9%       | 99.5%       |
| Storage cost    | High     | Medium      | Low         |
| Redundancy      | Multi-AZ | Multi-AZ    | Single AZ   |

#### Q38. Make objects private by default?
Disable public access at bucket/account level, IAM policy, no public ACL/bucket policy.

#### Q39. S3 Intelligent-Tiering?
Auto moves objects between frequent/infrequent tiers. Cost-effective for unpredictable workloads.

#### Q40. Scenario: 10 TB daily logs, cheap storage, retain 1 year, access occasionally?

- Create S3 bucket with versioning
- Lifecycle Policy: Move logs to Glacier after 30 days, delete after 1 year
- Enable encryption & bucket policies
- Use S3 analytics for usage

---

# AWS RDS & Aurora Interview FAQ

This file contains concise Q&A notes, tables, and scenario answers for Amazon RDS & Aurora.

---

## 🗄️ Amazon RDS & Amazon Aurora

### 1. What is Amazon RDS?
Managed relational database service (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server).

- Benefits: automatic backups, patching, Multi-AZ, read replicas.

#### Example
Launch RDS MySQL for web app—AWS handles backups, failover, updates.

---

### 2. What is Amazon Aurora?
AWS-designed relational DB, MySQL- and PostgreSQL-compatible, faster and highly available.

- 5x faster than MySQL, 3x faster than PostgreSQL
- Replicates across 3 AZs
- Storage auto-scales to 128 TB
- Supports Aurora Serverless (auto-scaling compute)

---

### Difference Between RDS and Aurora

| Feature           | Amazon RDS           | Amazon Aurora                 |
|-------------------|----------------------|-------------------------------|
| Engine            | MySQL, PostgreSQL, Oracle, SQL Server, MariaDB | MySQL-compatible, PostgreSQL-compatible |
| Performance       | Standard             | 3–5x faster                   |
| High Availability | Multi-AZ optional    | Multi-AZ default, highly durable |
| Storage Auto-Scaling | Limited           | Up to 128 TB automatically    |
| Read Scaling      | Read replicas        | Up to 15 read replicas        |
| Serverless        | No                   | Yes (Aurora Serverless)       |

---

### 3. Common Interview Questions & Answers

#### Q1. What is Amazon RDS?
Managed relational DB service. Handles provisioning, patching, backups, scaling.

#### Q2. What is Amazon Aurora?
High-performance, MySQL-/PostgreSQL-compatible DB designed by AWS. High availability, auto-scaling, faster.

#### Q3. What is Multi-AZ in RDS?
Deploy DB in two AZs for high availability; AWS auto failover if an AZ fails.

#### Q4. What are Read Replicas?
Copies optimized for read-heavy workloads; can be promoted to standalone.

#### Q5. What is Aurora Serverless?
Aurora auto-scales compute based on demand; cost-efficient for idle/variable workloads.

#### Q6. Aurora durability?
Replicates data across 3 AZs, continuous backup to S3, self-healing storage.

#### Q7. RDS Multi-AZ vs Read Replicas

| Feature      | Multi-AZ      | Read Replica           |
|--------------|---------------|------------------------|
| Purpose      | High availability | Read scaling        |
| Write/Read   | Supports writes & reads | Read-only      |
| Failover     | Automatic     | Manual promotion       |

#### Q8. Aurora max storage?
128 TB per cluster; auto-scaling.

#### Q9. Aurora MySQL vs RDS MySQL

| Feature      | RDS MySQL     | Aurora MySQL           |
|--------------|---------------|------------------------|
| Performance  | Standard      | 5x faster              |
| High Availability | Optional Multi-AZ | Multi-AZ default |
| Storage      | Max 64 TB     | Max 128 TB, auto-scale |
| Read Replicas| 5             | 15                     |

#### Q10. Aurora cross-region replication?
Yes (Aurora Global DB)—low-latency global reads, DR in other region.

#### Q11. Aurora Backups?
Continuous backup to S3, PITR supported, automatic snapshots.

#### Q12. RDS snapshots vs automated backups

| Feature          | Automated Backup | Manual Snapshot      |
|------------------|------------------|---------------------|
| Creation         | Automatic (daily)| User-initiated      |
| Retention        | 0–35 days        | Until deleted       |
| Restore          | Point-in-time    | At snapshot time    |

#### Q13. Scenario: Read-heavy MySQL app, slow queries?
- Use RDS/Aurora MySQL
- Enable Read Replicas
- Consider Aurora Serverless if load fluctuates
- Optimize queries/indexes

#### Q14. Scenario: Need highly available DB, auto failover?
- Aurora Multi-AZ (3 AZ replication)
- Automatic failover, minimal downtime
- Backups to S3

#### Q15. RDS vs Aurora scaling?
- **RDS**: Scale vertically (larger instance) or add read replicas
- **Aurora**: Scale vertically, horizontally (up to 15 replicas), auto-scaling storage

---

## 🗄️ Amazon RDS & Aurora — Advanced Q&A

#### Q16. How to secure RDS/Aurora?
- VPC isolation (private subnets)
- Security groups (restrict IP/EC2)
- Encryption at rest (KMS)
- Encryption in transit (SSL/TLS)
- IAM DB authentication
- Automated backups

#### Q17. Encryption at rest vs in transit

| Type      | Purpose                       |
|-----------|------------------------------|
| At rest   | Data stored on disk encrypted |
| In transit| Data sent over network encrypted|

#### Q18. What is RDS Performance Insights?
Monitors DB performance—slow queries, CPU, memory, connections. Works for RDS/Aurora.

#### Q19. Aurora Replicas vs RDS Read Replicas

| Feature      | RDS Read Replica | Aurora Replica         |
|--------------|------------------|-----------------------|
| Max replicas | 5                | 15                    |
| Failover     | Manual           | Automatic             |
| Latency      | Higher           | Low, built-in         |

#### Q20. Aurora failover?
Detects master failure, promotes replica in <30s, endpoint auto-updates.

#### Q21. Aurora for global apps?
Yes—Aurora Global DB for cross-region replication, low-latency reads, DR.

#### Q22. What is RDS Multi-AZ?
Synchronizes data to standby in another AZ; auto failover; high availability.

#### Q23. Multi-AZ vs Read Replica

| Feature      | Multi-AZ      | Read Replica           |
|--------------|---------------|------------------------|
| Purpose      | High availability | Read scaling        |
| Type         | Synchronous   | Asynchronous          |
| Read access  | Optional      | Yes (read-only)       |
| Failover     | Automatic     | Manual promotion      |

#### Q24. Aurora Backtracking?
Move back in time without restore; useful for accidental deletion—Aurora MySQL only.

#### Q25. Aurora max storage?
Auto-scales up to 128 TB per cluster.

#### Q26. DB migration to RDS/Aurora?
Use AWS DMS; supports homogeneous/heterogeneous migrations; minimal downtime.

#### Q27. Aurora Serverless v2?
Auto-scales compute/memory (1+ ACUs), fine-grained scaling, cost-efficient.

#### Q28. RDS instance classes vs Aurora instance classes

| Feature      | RDS            | Aurora                 |
|--------------|----------------|------------------------|
| Scaling      | Vertical       | Vertical+horizontal    |
| Storage      | Manual         | Auto-scale to 128 TB   |
| HA           | Multi-AZ opt.  | Multi-AZ built-in      |

#### Q29. Backup in RDS/Aurora?
Automated (daily, PITR), manual snapshots; Aurora: continuous backup to S3.

#### Q30. Scenario: Global e-commerce, HA, low-latency DB for multi-region users?
- Use Aurora Global DB
- Deploy Aurora Replicas in each region
- Enable backups/encryption
- Monitor with Performance Insights

#### Q31. Aurora fault tolerance?
Replicates data across 3 AZs; auto-replaces failed nodes; self-healing storage.

#### Q32. RDS snapshots vs Aurora continuous backup

| Feature      | RDS            | Aurora                 |
|--------------|----------------|------------------------|
| Backup type  | Automated/manual snapshot | Continuous to S3  |
| Recovery     | Restore snapshot| Point-in-time recovery |
| Granularity  | Daily          | Second-level           |

#### Q33. Aurora vs DynamoDB

| Feature   | Aurora           | DynamoDB                |
|-----------|------------------|-------------------------|
| Type      | Relational DB    | NoSQL key-value/document|
| Use Case  | Transactions, queries | Massive scale, fast ops|
| Scaling   | Read replicas, auto-storage| Auto-scale throughput|
| Query     | SQL              | DynamoDB API            |

#### Q34. Monitor Aurora/RDS performance?
- CloudWatch metrics
- Enhanced Monitoring (OS-level)
- Performance Insights (query-level)
- Event Subscriptions

#### Q35. Scenario: MySQL DB, heavy reads, low writes
- Use Aurora/RDS
- Add Read Replicas
- Primary DB for writes
- Aurora Serverless if load varies

---

# AWS Route 53 Interview FAQ

This file contains concise Q&A notes, tables, and scenario answers for Amazon Route 53.

---

## 🌐 Amazon Route 53

### 1. What is Amazon Route 53?
Highly available, scalable DNS service. Main features:
- Route users to websites/apps
- Register domain names
- Monitor health of endpoints

**Simple analogy:** Like the internet's phonebook — converts domain names to IP addresses.

#### Example
- Website hosted on EC2 IP `18.215.12.10`
- Register domain `mywebsite.com` in Route 53
- Route 53 maps domain to EC2 IP

---

### 2. Key Concepts of Route 53

| Component     | Description                        | Example              |
|---------------|------------------------------------|----------------------|
| Hosted Zone   | Container for DNS records          | mywebsite.com        |
| DNS Record    | Maps domain/subdomain to IP/AWS svc| A, CNAME, MX records |
| Record Types  | Types of DNS records               | A, AAAA, CNAME, MX, TXT, NS |
| Health Check  | Monitors endpoint availability     | Ping server, failover|
| Traffic Policy| Routing traffic                    | Weighted, latency, geo|
| Domain Reg.   | Register domain in AWS             | example.com          |

---

### 3. Route 53 Routing Policies

| Policy          | Description                           | Example                                        |
|-----------------|---------------------------------------|------------------------------------------------|
| Simple          | Routes to single resource             | One EC2                                        |
| Weighted        | Distributes traffic across resources  | 70% to EC2-A, 30% to EC2-B                     |
| Latency-based   | Routes to lowest-latency region       | US users → US-East, EU users → EU-West         |
| Failover        | Redirects if primary fails            | Web down → redirect to backup                   |
| Geolocation     | User location-based routing           | India users → India server                      |
| Geoproximity    | Distance-based routing                | Closest region gets traffic                     |
| Multi-value     | Returns multiple IPs (health checked) | DNS-level load balancing                        |

---

### 4. Common Interview Q&A

#### Q1. What is Route 53?
DNS service for domain registration, routing, health checks.

#### Q2. What is a Hosted Zone?
Container for DNS records for a domain (e.g., `mywebsite.com`).

#### Q3. DNS record types

| Record | Purpose                              |
|--------|--------------------------------------|
| A      | Domain → IPv4 address                |
| AAAA   | Domain → IPv6 address                |
| CNAME  | Subdomain → another domain           |
| MX     | Mail server for domain               |
| TXT    | Text info, SPF/DKIM                  |
| NS     | Nameserver record                    |
| SRV    | Service location                     |
| Alias  | AWS: domain → AWS resource (ELB, S3) |

#### Q4. Alias record in Route 53?
AWS-specific. Maps domain/subdomain directly to AWS resources (ELB, CloudFront, S3). Free DNS query charges, works at root domain.

#### Q5. Route 53 Health Check?
Monitors resource health (EC2, ELB, IP), can trigger failover.

#### Q6. Routing policies in Route 53?
Simple, Weighted, Latency-based, Failover, Geolocation, Geoproximity, Multi-value answer.

#### Q7. A Record vs CNAME

| Feature   | A Record     | CNAME Record         |
|-----------|--------------|---------------------|
| Maps to   | IP address   | Another domain      |
| Root use  | Yes          | No                  |
| Use case  | Main domain  | Subdomain redirect  |

#### Q8. Alias Record vs CNAME

| Feature      | Alias Record         | CNAME                  |
|--------------|---------------------|------------------------|
| AWS support  | Yes (ELB, S3, CF)   | No                     |
| Root domain  | Yes                 | No                     |
| Free DNS     | Yes                 | No                     |

#### Q9. How does failover work?
Primary and secondary endpoints. Health check on primary; auto-switch to secondary on failure.

#### Q10. Latency-based routing?
Routes users to region with lowest latency for faster response.

#### Q11. Weighted routing?
Proportional traffic split (e.g., 70/30 between EC2s).

#### Q12. Geolocation vs Geoproximity

| Routing         | Description                  |
|-----------------|-----------------------------|
| Geolocation     | By continent/country         |
| Geoproximity    | By distance from region      |

#### Q13. Can Route 53 register domains?
Yes—register/manage domains (.com, .org, .net) integrated with DNS records.

#### Q14. Route 53 with S3 static websites?
Yes—use Alias record to point domain to S3 website endpoint.

#### Q15. Scenario: Multi-region app, slow access?
- Use latency-based routing
- Health checks for endpoints
- Optionally, weighted routing for testing
- Enable CloudFront CDN

#### Q16. Scenario: Ensure website always available (EC2 failover)?
- Use failover routing
- Health check on primary EC2
- Secondary EC2 in another AZ
- Auto-switch on failure

---

## 🌐 Amazon Route 53 — Advanced Q&A

#### Q17. Public vs Private hosted zones

| Feature         | Public Hosted Zone   | Private Hosted Zone    |
|-----------------|---------------------|------------------------|
| Accessibility   | Internet            | Only within VPC(s)     |
| Use case        | Websites, global    | Internal apps/services |
| DNS resolution  | Public DNS          | Private DNS            |

#### Q18. Private hosted zone with multiple VPCs?
Yes—can associate with multiple VPCs (even across accounts).

#### Q19. What is a CAA record?
Specifies which CA can issue SSL/TLS certificates for a domain.

#### Q20. Failover routing policy?
Routes to primary resource; auto-switch to secondary on failure (health check driven).

#### Q21. Multi-value answer routing policy?
Returns multiple healthy IPs—DNS-level load balancing, integrates with health checks.

#### Q22. Route 53 with CloudFront?
Use Alias record to point domain to CloudFront; free DNS queries, fast global delivery.

#### Q23. NS vs SOA records

| Record | Purpose                                |
|--------|----------------------------------------|
| NS     | Authoritative DNS servers for domain   |
| SOA    | Domain admin info, primary NS, serial  |

#### Q24. Health checks on non-AWS endpoints?
Yes—monitor on-prem, external EC2, any public IP.

#### Q25. Latency-based vs Weighted routing

| Routing      | Use case                | Traffic distribution         |
|--------------|------------------------|------------------------------|
| Latency-based| Optimize response time  | Route to lowest-latency region|
| Weighted     | Gradual rollout/testing | Percentage split across endpoints|

#### Q26. Scenario: Route Europe users to EU servers, US to US servers?
- Use geolocation routing
- Records for EU/US endpoints
- Default record for other users

#### Q27. Scenario: Gradually migrate to new EC2 without downtime?
- Use weighted routing (e.g., 90% old, 10% new)
- Gradually increase new EC2 share
- Final: 100% to new EC2

#### Q28. Geolocation vs Geoproximity

| Routing        | Description                                   |
|----------------|----------------------------------------------|
| Geolocation    | Based on continent/country                    |
| Geoproximity   | Based on distance from AWS region (Traffic Flow)|

#### Q29. Common use cases for Route 53
- Hosting site/app domain
- DNS failover for high availability
- Latency-based routing for global apps
- Integrate with CloudFront/S3
- Internal DNS with private hosted zones

#### Q30. High availability in Route 53?
- Global distribution
- Redundant DNS servers
- Automatic failover with health checks
- Auto-scaled query handling

#### Q31. Route 53 Traffic Flow Policy?
Visual tool for complex routing—combine latency, weighted, failover, geoproximity; supports multi-region/multi-account.

#### Q32. Latency alias record?
Alias record used with latency routing; points domain/subdomain to AWS resource in lowest-latency region.

#### Q33. Migrating DNS to Route 53?
- Create hosted zone
- Create DNS records matching old provider
- Update registrar NS records to Route 53
- Optional: test TTL propagation

#### Q34. TTL in Route 53 DNS records?
Time To Live—how long DNS responses are cached.
- Lower TTL: faster changes
- Higher TTL: less DNS traffic

#### Q35. Scenario: Critical web app, 24/7, EC2 in two regions?
- Failover routing with health checks
- Primary EC2 in main region, secondary backup region
- Latency-based routing for global users
- Multi-value answer for intra-region load balancing

---

# AWS CloudWatch Interview FAQ

This file contains concise Q&A notes, tables, and scenario answers for Amazon CloudWatch.

---

## ☁️ Amazon CloudWatch

### 1. What is Amazon CloudWatch?
Monitoring and observability service for AWS resources and applications.

- Collect & track metrics (CPU, memory, network, custom)
- Monitor logs (EC2, Lambda, app logs)
- Set alarms (notify/trigger on thresholds)
- Automate actions (scale, recover, notify)

**Simple analogy:** CloudWatch is your AWS health dashboard.

#### Example
EC2 running web server: CloudWatch tracks CPU, memory, disk I/O. Alarm: CPU > 80% for 5 min → Auto Scaling adds EC2.

---

### 2. Key Components of CloudWatch

| Component      | Description                      | Example                       |
|----------------|----------------------------------|-------------------------------|
| Metrics        | Numerical data for resources     | CPU utilization, network in/out|
| Logs           | Application/system logs          | EC2 syslog, Lambda logs       |
| Alarms         | Trigger actions on metrics       | CPU > 80% → scale out         |
| Dashboards     | Visual graphs of metrics         | Web UI graphs                 |
| Events         | Detect resource changes          | EC2 stop/start, Lambda invoke |
| Agent          | Collect OS-level/custom metrics  | Memory, disk, app metrics     |

---

### 3. CloudWatch Metrics Types

| Metric Type         | Description                    | Example                |
|---------------------|-------------------------------|------------------------|
| Basic Metrics       | Default AWS resource metrics   | EC2 CPU, Network       |
| Custom Metrics      | User-defined metrics           | App request count      |
| High-Resolution     | 1-second granularity           | Rapid scaling decisions|

---

### 4. Common Interview Q&A

#### Q1. What is Amazon CloudWatch?
AWS monitoring/logging/alarms/dashboards for resources/apps.

#### Q2. What are CloudWatch metrics?
Numerical measurements—CPU, memory, disk, etc.

#### Q3. What are CloudWatch logs?
Text data from resources/apps—EC2 syslog, Lambda logs, etc.

#### Q4. What is a CloudWatch Alarm?
Monitors a metric, triggers actions (e.g., CPU > 80% → SNS/scale out).

#### Q5. What is a CloudWatch Dashboard?
Visual graphs/widgets for metrics and alarms.

#### Q6. CloudWatch vs CloudTrail

| Feature   | CloudWatch            | CloudTrail                 |
|-----------|----------------------|----------------------------|
| Purpose   | Metrics/logs/monitor | Tracks API calls/actions   |
| Data      | Performance metrics  | Event history of API calls |
| Use case  | Scaling, dashboards  | Security auditing          |

#### Q7. CloudWatch vs X-Ray

| Feature   | CloudWatch        | X-Ray                   |
|-----------|------------------|-------------------------|
| Purpose   | Metrics, logs    | Application tracing     |
| Data      | CPU, memory, logs| Request traces/errors   |
| Use case  | Auto scaling     | Debugging microservices |

#### Q8. What is CloudWatch Events / EventBridge?
Detects AWS resource changes, triggers actions (Lambda, SNS, SQS).

#### Q9. What are CloudWatch custom metrics?
User/app-defined metrics—e.g., orders processed, logins, errors.

#### Q10. How does CloudWatch scale EC2 automatically?
Create alarm on metric, connect to Auto Scaling group.

#### Q11. What is the CloudWatch agent?
Installed on EC2/on-prem servers, collects OS-level/custom metrics.

#### Q12. CloudWatch Logs retention?
Default: indefinite. Configurable deletion after N days (cost control).

#### Q13. CloudWatch pricing?
Based on metrics, alarms, logs, dashboards. Free tier: 10 custom metrics, 5GB logs/month.

#### Q14. Scenario: EC2 CPU spikes—how to handle?
- Create metric/alarm for CPU > 80%
- Connect alarm to Auto Scaling group
- Monitor logs for root cause

#### Q15. Scenario: Monitor memory usage (not default)?
- Install CloudWatch Agent
- Configure agent for memory/disk metrics
- Push to CloudWatch, create alarms

#### Q16. CloudWatch Metrics vs Logs

| Feature   | Metrics           | Logs                  |
|-----------|-------------------|-----------------------|
| Data      | Numerical         | Text                  |
| Granularity| Seconds/minutes  | Raw events            |
| Use       | Alarms/dashboards | Debugging             |

#### Q17. Alarms vs EventBridge

| Feature    | CloudWatch Alarms   | CloudWatch Events/EventBridge |
|------------|--------------------|-------------------------------|
| Trigger    | Metric thresholds   | Resource changes/schedule     |
| Action     | Scale, notify       | Lambda, SNS, SQS              |
| Example    | CPU > 80% → scale   | EC2 stopped → backup Lambda   |

#### Q18. CloudWatch Contributor Insights?
Analyzes high-cardinality log data—identifies top contributors (e.g., IPs causing errors).

#### Q19. CloudWatch Anomaly Detection?
Detects unusual metric behavior (ML)—e.g., CPU spikes.

#### Q20. Scenario: Lambda app—monitor performance/errors?
- Enable CloudWatch Logs
- Track invocations/errors/duration in Metrics
- Create alarms for errors
- Use dashboards for visualization

---

## ☁️ Amazon CloudWatch — Advanced Q&A

#### Q21. Standard vs High-res metrics

| Feature     | Standard Metrics | High-Resolution Metrics |
|-------------|-----------------|------------------------|
| Granularity | 1-minute        | 1-second               |
| Use case    | Regular monitor | Rapid scaling/real-time|
| Cost        | Lower           | Higher                 |

#### Q22. CloudWatch monitor on-premises?
Yes—install agent on on-prem servers, push metrics to CloudWatch.

#### Q23. CloudWatch Logs Insights?
Interactive query tool—find patterns/troubleshoot in logs (e.g., count 500 errors).

#### Q24. Contributor Insights?
Analyzes high-cardinality data—top contributors to metrics/issues.

#### Q25. CloudWatch Logs vs CloudTrail

| Feature   | CloudWatch Logs | CloudTrail             |
|-----------|----------------|------------------------|
| Purpose   | App/system logs| Tracks AWS API calls   |
| Data      | Metrics, logs  | Resource activity      |
| Use       | Monitoring     | Security auditing      |

#### Q26. Can CloudWatch trigger actions automatically?
Yes—Alarms trigger SNS, Auto Scaling, Lambda.

#### Q27. EventBridge best use cases?
Respond to resource changes, schedule tasks, trigger Lambda/SQS/SNS.

#### Q28. CloudWatch Anomaly Detection?
ML models on metrics—detects deviations (CPU spikes, API rates).

#### Q29. CloudWatch for cost optimization?
Track underutilized resources, set alarms for idle resources, integrate with scaling.

#### Q30. Alarms vs Events

| Feature    | CloudWatch Alarm   | CloudWatch Event/EventBridge |
|------------|-------------------|-----------------------------|
| Trigger    | Metric thresholds | Resource/state/schedule     |
| Action     | Auto Scaling, SNS | Lambda, SQS, SNS            |

#### Q31. Scenario: EC2 CPU > 80%, auto scale & notify team?
- Metric for CPU
- Alarm for > 80%
- Connect to Auto Scaling
- SNS notification for team

#### Q32. Scenario: Monitor Lambda errors & visualize?
- Enable Logs for Lambda
- Track errors/invocations/duration
- Create dashboard with metrics
- Set alarms as needed

#### Q33. Scenario: RDS CPU spikes, analyze root cause?
- Enable Enhanced Monitoring
- Track CPU, memory, disk I/O
- Use Logs Insights for query analysis
- Set alarms for thresholds

#### Q34. Dashboards vs Metrics

| Feature      | Metrics            | Dashboards              |
|--------------|-------------------|-------------------------|
| Purpose      | Collect/store      | Visualize in graphs     |
| Granularity  | 1s/1m              | Customizable            |

#### Q35. Contributor Insights vs Logs Insights

| Feature         | Contributor Insights     | Logs Insights              |
|-----------------|-------------------------|----------------------------|
| Purpose         | Top contributors        | Query log data             |
| Use case        | Top IPs causing errors  | Find error patterns/trends |

#### Q36. CloudWatch Logs retention policy?
Default: indefinite; configurable (1 day to 10 years) for cost control.

---

# AWS CloudFront Interview FAQ

Concise Q&A, tables, and scenarios for Amazon CloudFront.

---

## 🌐 Amazon CloudFront

### 1. What is Amazon CloudFront?
Content Delivery Network (CDN) that delivers web content, APIs, videos, and apps with low latency and high speed.

- Uses global edge locations
- Caches static/dynamic content close to users
- Integrates with S3, EC2, Lambda@Edge, API Gateway

**Simple analogy:** CloudFront makes your site/app load faster for global users by serving content from nearby locations.

#### Example
- S3 static site hosted in Mumbai
- US users see latency
- CloudFront caches content in US edge locations → faster access

---

### 2. Key Components of CloudFront

| Component        | Description                 | Example                      |
|------------------|----------------------------|------------------------------|
| Edge Location    | Data center close to users  | US-East, EU-West             |
| Origin           | Source of content           | S3 bucket, EC2, ALB          |
| Distribution     | Delivery config             | Web/RTMP distribution        |
| Cache Behavior   | How requests are handled    | Forward headers/cookies      |
| Invalidation     | Remove cached objects       | After updating S3 content    |
| Lambda@Edge      | Run code at edge locations  | Auth headers, personalization|

---

### 3. Distribution Types

| Type             | Use Case                      |
|------------------|------------------------------|
| Web Distribution | Websites, APIs, HTTP/HTTPS   |
| RTMP Distribution| Streaming media (legacy)     |

---

### 4. Common Interview Q&A

#### Q1. What is Amazon CloudFront?
AWS CDN—delivers content globally with low latency via edge locations.

#### Q2. Benefits of CloudFront?
Low latency, high speed, security (WAF/Shield/HTTPS), scalability, cost optimization.

#### Q3. CloudFront vs S3

| Feature   | S3              | CloudFront           |
|-----------|-----------------|----------------------|
| Purpose   | Object storage  | Content delivery     |
| Access    | Region direct   | Cached at edge       |
| Latency   | Region-based    | Low, global          |

#### Q4. What is Distribution?
Config for how CloudFront serves content—origin, caching, SSL, policies.

#### Q5. What is Origin?
Source of content (S3, EC2, ELB, API Gateway).

#### Q6. What is Edge Location?
Datacenter near users, serves cached content.

#### Q7. What is Cache Behavior?
How CloudFront handles requests—forward headers/cookies/query strings, TTL.

#### Q8. What is Invalidation?
Remove cached objects before TTL expires (updates). May incur cost.

#### Q9. What is Lambda@Edge?
Run code at edge locations (auth, header rewrite, personalization) for lower latency.

#### Q10. How does CloudFront improve security?
- HTTPS support
- AWS WAF for attacks
- AWS Shield for DDoS
- Signed URLs/cookies for access control

#### Q11. CloudFront vs ELB

| Feature   | CloudFront          | ELB                      |
|-----------|---------------------|--------------------------|
| Purpose   | Content delivery    | Load balancing           |
| Latency   | Edge locations      | Region-based             |
| Use Case  | Global caching      | Distribute traffic       |

#### Q12. Dynamic content handling?
Cache with short TTL, forward cookies/headers, lower origin load.

#### Q13. Cost reduction?
Cache at edge (less origin requests), S3 origin (cheaper than EC2), reduce origin data transfer.

#### Q14. Scenario: Global S3 site, slow outside India?
- Create CloudFront distribution (S3 origin)
- Enable global caching
- Enable HTTPS
- Optionally use Lambda@Edge

#### Q15. Scenario: Users see old content after update?
- Invalidate cached objects
- Wait for propagation
- Optionally, reduce TTL

#### Q16. CloudFront vs Route 53

| Feature   | CloudFront           | Route 53          |
|-----------|----------------------|-------------------|
| Purpose   | Content delivery     | DNS service       |
| Function  | Caches/serves content| Routes users      |
| Integration| S3, EC2, Lambda     | Maps domains      |

#### Q17. Can CloudFront work with APIs?
Yes—API Gateway or ALB as origin, cache GET requests.

#### Q18. What is Origin Shield?
Regional caching layer, reduces origin fetch, improves cache hit ratio.

#### Q19. CloudFront for dynamic websites?
Cache static assets at edge, forward dynamic requests, use Lambda@Edge for personalization.

#### Q20. Scenario: Video streaming platform, global buffering?
- CloudFront with S3/media server origin
- Edge caching for popular videos
- Use RTMP/HLS if needed
- Monitor with CloudWatch

---

## 🌐 Amazon CloudFront — Advanced Q&A

#### Q21. Signed URL or Cookie?
Restricted access (specific file/multiple files/site)—used for paid/download content.

#### Q22. Distribution vs Origin

| Feature        | Distribution           | Origin                  |
|----------------|-----------------------|-------------------------|
| Purpose        | Delivery config        | Source of content       |
| Components     | Cache, SSL, TTL       | S3, EC2, ALB, API GW    |

#### Q23. What is Origin Access Identity (OAI)?
Special CloudFront user for S3 access—prevents direct S3 public access.

#### Q24. HTTPS in CloudFront?
Supports SSL/TLS—use default (*.cloudfront.net) or custom ACM cert.

#### Q25. CloudFront + WAF?
Attach WAF to distribution—block web attacks (SQLi, XSS, bots).

#### Q26. Cache TTL?
How long objects stay cached; short for frequent updates, long for static content.

#### Q27. CloudFront vs Traditional CDN

| Feature     | CloudFront        | Traditional CDN         |
|-------------|-------------------|------------------------|
| Integration | AWS-integrated    | Independent            |
| Security    | WAF, Shield       | Third-party tools      |
| Pricing     | Pay-per-use       | Subscription           |
| Edge locs   | 450+ globally     | Fewer                  |

#### Q28. Scenario: S3 site, slow in Europe?
- Create CloudFront web distribution (S3 origin)
- Global edge caching
- Enable gzip compression
- Use HTTPS + custom domain via Route 53

#### Q29. Scenario: API on API Gateway, reduce global latency?
- CloudFront distribution (API GW origin)
- Cache GET requests
- Forward needed headers/query strings
- Monitor via CloudWatch

#### Q30. CloudFront for DDoS protection?
Integrates with AWS Shield; edge absorbs/filters traffic; WAF for malicious requests.

#### Q31. Web vs RTMP Distribution

| Feature     | Web Distribution | RTMP Distribution      |
|-------------|-----------------|------------------------|
| Use case    | Websites, APIs  | Streaming (Flash)      |
| Protocol    | HTTP/HTTPS      | RTMP                   |
| Status      | Standard        | Legacy                 |

#### Q32. Lambda@Edge for Personalization?
Modify content before delivery—country-specific, auth headers, etc.

#### Q33. What is Origin Shield?
Optional regional caching—reduces requests to origin, improves cache hit/latency.

#### Q34. Scenario: Updated images, users see old?
- Invalidate CloudFront files
- Reduce TTL if needed
- Wait for propagation

#### Q35. Monitor CloudFront performance?
Use CloudWatch metrics (requests, bytes, errors, hit/miss, latency), CloudFront logs.

#### Q36. CloudFront vs S3 Transfer Acceleration

| Feature     | CloudFront             | S3 Transfer Acceleration |
|-------------|------------------------|--------------------------|
| Purpose     | Global content delivery| Faster S3 uploads        |
| Direction   | Download to users      | Upload to S3             |
| Edge cache  | Yes                    | No                       |

---

# AWS Lambda Interview FAQ

This file contains concise Q&A notes, tables, and scenario answers for AWS Lambda.

---

## ⚡ AWS Lambda

### 1. What is AWS Lambda?
Serverless compute service to run code without managing servers.

- Pay for compute time (per request & duration)
- Auto scales with requests
- Triggered by AWS services, HTTP requests, schedules

**Simple analogy:** Lambda is a cloud function that runs only when needed; no server management.

#### Example
S3 uploads → Lambda resizes images → stores in another bucket.

---

### 2. Key Concepts of Lambda

| Component        | Description                          | Example                          |
|------------------|--------------------------------------|----------------------------------|
| Function         | Code to execute                      | resizeImage                      |
| Trigger/Event    | What invokes function                | S3, API GW, CloudWatch, DynamoDB |
| Runtime          | Language environment                 | Python, Node.js, Java, Go, .NET  |
| Handler          | Entry point                          | index.handler                    |
| Execution Role   | IAM role Lambda assumes              | S3/DynamoDB access permissions   |
| Layers           | Shared libraries across functions    | Logging lib, SDK                 |
| Concurrency      | Simultaneous executions              | Default 1000, adjustable         |

---

### 3. Lambda Use Cases

- File processing (S3 triggers)
- Real-time data (Kinesis, DynamoDB Streams)
- API backend (API Gateway)
- Scheduled tasks (CloudWatch Events/EventBridge)
- Automation (infra changes, backups, notifications)

---

### 4. Common Interview Q&A

#### Q1. What is AWS Lambda?
Serverless compute, runs code on events—no need to manage servers.

#### Q2. Lambda pricing?
Pay for requests and duration (GB-seconds). Free: 1M requests/month, 400k GB-seconds.

#### Q3. What triggers Lambda?
S3, API Gateway, DynamoDB Streams, Kinesis, CloudWatch Events, SNS, SQS, etc.

#### Q4. Lambda vs EC2

| Feature              | Lambda         | EC2                  |
|----------------------|---------------|----------------------|
| Server management    | None          | Full control         |
| Scaling              | Automatic     | Manual/Auto Scaling  |
| Pricing              | Pay per exec  | Pay per instance     |
| Use case             | Event-driven  | Long-running apps    |

#### Q5. Lambda execution role?
IAM role for Lambda; grants permissions to AWS services.

#### Q6. Lambda Layer?
ZIP package with libraries/shared code; attach to multiple functions.

#### Q7. What is cold start?
Initial delay after inactivity (container provision). Mitigate with Provisioned Concurrency.

#### Q8. Max execution duration?
15 minutes per invocation.

#### Q9. Deployment package options?
ZIP file (code + deps), Container image (up to 10 GB, custom runtime).

#### Q10. Synchronous vs Asynchronous invocation

| Feature                | Synchronous    | Asynchronous         |
|------------------------|---------------|----------------------|
| Caller waits           | Yes           | No                   |
| Example                | API GW → Lambda| S3 event → Lambda    |
| Retry behavior         | Caller retries| AWS retries          |

#### Q11. Lambda scaling?
Auto horizontal scaling per incoming events. Default concurrency: 1000.

#### Q12. Lambda@Edge?
Run Lambda at CloudFront edge locations. Use for auth, header manipulation, personalization.

#### Q13. Scenario: Resize S3 images
- Lambda function resizes images
- Execution role with S3 permissions
- S3 event triggers Lambda

#### Q14. Scenario: Lambda runs hourly
- CloudWatch Event/EventBridge rule (cron)
- Lambda as target

#### Q15. Scenario: Slow initial API response
- Cold start likely
- Enable Provisioned Concurrency

#### Q16. Lambda vs ECS/Fargate

| Feature     | Lambda      | ECS/Fargate                  |
|-------------|------------|------------------------------|
| Serverless  | Yes        | Yes (Fargate), No (ECS EC2)  |
| Duration    | Max 15 min | Long-running                 |
| Use case    | Event-driven| Microservices, batch jobs    |

#### Q17. Lambda in VPC?
Attach VPC config; Lambda gets ENI, can access private subnets/resources.

#### Q18. Lambda vs Step Functions

| Feature     | Lambda            | Step Functions       |
|-------------|-------------------|---------------------|
| Purpose     | Single function   | Orchestrate workflow|
| Duration    | Up to 15 min      | Long-running        |
| Use case    | Event-driven      | ETL, orchestration  |

#### Q19. Lambda Destinations?
Where async Lambda results go: SQS, SNS, Lambda, EventBridge.

#### Q20. Lambda best practices?
Small, focused functions; config via env vars; monitor CloudWatch; avoid long-running tasks; use Layers.

---

## ⚡ AWS Lambda — Advanced Q&A

#### Q21. Lambda vs EC2 scaling

| Feature        | Lambda             | EC2                   |
|----------------|--------------------|-----------------------|
| Scaling        | Automatic, event   | Manual/Auto Scaling   |
| Billing        | Per request/time   | Per running instance  |
| Duration       | Max 15 min         | Long-running          |
| Server mgmt    | Serverless         | Full control          |

#### Q22. Provisioned Concurrency?
Keeps pool of pre-initialized Lambdas ready; eliminates cold starts.

#### Q23. Environment Variables?
Key-value pairs for config (DB_HOST, API_KEY).

#### Q24. Max deployment package size?

| Deployment Type   | Max Size               |
|-------------------|------------------------|
| ZIP file          | 50 MB (zip), 250 MB unzipped|
| Container image   | 10 GB                  |

#### Q25. Concurrency limits?
Default: 1000 concurrent. Can increase. Reserved/provisioned concurrency options.

#### Q26. Synchronous vs Asynchronous invocation (again)

| Feature       | Synchronous         | Asynchronous          |
|---------------|---------------------|-----------------------|
| Caller waits  | Yes                 | No                    |
| Error handle  | Immediate           | DLQ (optional)        |

#### Q27. Dead Letter Queue (DLQ)?
Failed async events go to SQS/SNS for debugging.

#### Q28. Lambda + CloudWatch?
Logs: Execution/errors/print
Metrics: Invocations, errors, duration, throttles, concurrency
Alarms: Trigger SNS, scaling

#### Q29. Event Source Mapping?
For streams (DynamoDB/Kinesis); Lambda polls & invokes automatically.

#### Q30. Scenario: API sluggish at peak
- Enable Provisioned Concurrency
- Optimize code/deps
- Use smaller package
- Monitor with CloudWatch
- Use Lambda@Edge if global

#### Q31. Scenario: S3 uploads, retry on failure
- S3 triggers Lambda (async)
- Enable DLQ (SQS/SNS)
- Use Lambda Destinations

#### Q32. Scenario: Nightly batch job at 2 AM
- CloudWatch Event/EventBridge (cron: 0 2 * * ? *)
- Lambda target
- Proper execution role

#### Q33. Handling large payloads?
Max event: 6MB sync, 256KB async. For more, store in S3, pass key to Lambda.

#### Q34. Lambda SnapStart?
Optimizes Java Lambdas; pre-initializes env; reduces cold starts.

#### Q35. Lambda with VPC resources?
Configure VPC settings; Lambda gets ENI; access private subnets/resources.

#### Q36. Orchestrate multiple Lambdas/workflow?
Use AWS Step Functions; define retries/error handling; monitor workflow.

#### Q37. Lambda vs Fargate

| Feature     | Lambda    | Fargate                   |
|-------------|-----------|---------------------------|
| Serverless  | Yes       | Yes (containers)          |
| Duration    | Max 15min | Long-running              |
| Scaling     | Automatic | Automatic (slower)        |
| Use case    | Event     | Microservices, batch      |

#### Q38. Improving Lambda security?
Minimal IAM role permissions; encrypt env vars; VPC integration; CloudWatch logging/auditing.

---

# AWS CloudFormation Interview FAQ

This file contains concise Q&A notes, tables, and scenario answers for AWS CloudFormation.

---

## 🏗️ AWS CloudFormation

### 1. What is AWS CloudFormation?
Define and provision AWS infrastructure using code (YAML/JSON templates).

- Automatically creates, updates, deletes AWS resources
- Supports almost all AWS services

**Simple analogy:** CloudFormation is a blueprint—write a template, AWS builds your resources.

#### Example
Need 3 EC2s, VPC, S3 bucket? Write template, deploy—AWS provisions all in order.

---

### 2. Key Concepts

| Component     | Description                       | Example                        |
|---------------|-----------------------------------|--------------------------------|
| Template      | Defines resources/config           | YAML/JSON file: EC2, S3, VPC   |
| Stack         | Deployed resources from template   | Stack "MyApp": EC2+S3          |
| StackSet      | Stack across multiple accounts     | Multi-region web app           |
| Change Set    | Preview changes before updating    | Add EC2, see impact            |
| Resource      | Individual AWS component           | EC2, S3, IAM role              |
| Parameter     | Input value for template           | Instance type, key pair        |
| Output        | Value returned after creation      | EC2 DNS, S3 bucket name        |

---

### 3. CloudFormation Benefits

- Automation (no manual resource creation)
- Consistency (same template = same resources)
- Version control (store templates in Git)
- Rollback on failure
- Multi-region/account deployment (StackSets)

---

### 4. Common Interview Q&A

#### Q1. What is AWS CloudFormation?
Infrastructure as Code—automated AWS resource creation/management via YAML/JSON templates.

#### Q2. Stack vs StackSet

| Feature   | Stack                | StackSet                    |
|-----------|----------------------|-----------------------------|
| Scope     | Single region/account| Multiple regions/accounts   |
| Use case  | Deploy app resources | Multi-region app            |
| Example   | MyApp in us-east-1   | StackSet in us-east-1, eu-west-1|

#### Q3. CloudFormation template?
File in JSON/YAML, defines resources/config. Sections: Resources, Parameters, Outputs, Mappings, Conditions.

#### Q4. Change Set?
Preview changes before updating stack; prevents accidental modification/deletion.

#### Q5. Parameters?
Input values at stack creation (InstanceType, KeyName).

#### Q6. Outputs?
Values returned after stack creation (EC2 DNS, S3 bucket).

#### Q7. Dependencies?
CloudFormation auto-determines resource creation order via references (VPC → Subnet → EC2).

#### Q8. CloudFormation vs Terraform

| Feature         | CloudFormation    | Terraform                   |
|-----------------|------------------|-----------------------------|
| Provider        | AWS only         | Multi-cloud                 |
| Language        | YAML/JSON        | HCL                         |
| State           | AWS managed      | User/remote backend         |
| Modules         | AWS-only         | Multi-cloud                 |

#### Q9. Stack policy?
Protects specific resources during updates (e.g., prevent RDS deletion).

#### Q10. Nested vs normal stack

| Feature      | Normal Stack       | Nested Stack                |
|--------------|-------------------|-----------------------------|
| Purpose      | Single template    | Reuse templates inside main |
| Example      | EC2 + S3          | Main stack: VPC stack + App stack|

#### Q11. Scenario: EC2s in different regions?
- CloudFormation template for EC2s
- StackSets to deploy in multiple regions/accounts

#### Q12. Scenario: Prevent accidental RDS deletion?
- Apply stack policy
- Review Change Set before update
- Use rollback on failure

#### Q13. Drift Detection?
Detects manual changes to resources outside CloudFormation; ensures stack state matches template.

#### Q14. Template sections?
- AWSTemplateFormatVersion
- Description
- Parameters
- Mappings
- Conditions
- Resources (mandatory)
- Outputs

#### Q15. CloudFormation for DevOps?
Enables infrastructure as code, supports CI/CD pipelines, version control, reduces manual errors.

---

## 🏗️ AWS CloudFormation — Advanced Q&A

#### Q16. Mappings?
Define fixed values (e.g., region → AMI ID):

```yaml
Mappings:
  RegionMap:
    us-east-1:
      AMI: ami-0abcdef12345
    eu-west-1:
      AMI: ami-0fedcba54321
```
Use with !FindInMap.

#### Q17. Conditions?
Create resources based on criteria (e.g., only in prod):

```yaml
Conditions:
  CreateProdResources: !Equals [ !Ref EnvType, prod ]
```
Use with !If.

#### Q18. Safe stack update?
- Create Change Set
- Review changes
- Apply
- Use stack policies for protection

#### Q19. Update Stack vs Replace Stack

| Feature    | Update Stack      | Replace Stack              |
|------------|-------------------|----------------------------|
| Purpose    | Modify resources  | Delete old, create new     |
| Risk       | Lower             | Higher, may destroy        |
| Use case   | Add EC2           | Major re-architecture      |

#### Q20. Stack creation fails?
CloudFormation rolls back by default; deletes created resources; prevents partial deployments.

#### Q21. CloudFormation vs Elastic Beanstalk

| Feature      | CloudFormation    | Elastic Beanstalk         |
|--------------|------------------|---------------------------|
| Purpose      | Infra as code     | Platform as a Service     |
| Control      | Full resource ctrl| Limited resource ctrl     |
| Use case     | Multi-resource    | Web app deployment        |
| Automation   | Template-based    | Managed environment       |

#### Q22. Multi-account deployments?
Use StackSets for standardized infra across accounts/regions.

#### Q23. Drift Detection (again)?
Ensures resources match template; audits compliance.

#### Q24. Scenario: Multi-env (dev, test, prod) with differences?
- Use Parameters for env-specific values
- Mappings for region-specific (e.g., AMIs)
- Conditions for optional resources
- Deploy separate stacks per env

#### Q25. Scenario: Update stack, protect critical resources?
- Create Change Set to preview
- Apply Stack Policies
- Monitor and verify outputs

#### Q26. Resource dependencies?
CloudFormation auto-creates based on references (!Ref, !GetAtt).

#### Q27. Resource update vs replacement

| Feature   | Update           | Replacement              |
|-----------|------------------|--------------------------|
| Action    | Modify in place  | Delete + create new      |
| Risk      | Low              | Higher, possible downtime|
| Example   | Change EC2 tags  | Change EC2 type (replace)|

#### Q28. CloudFormation in CI/CD?
- Store templates in Git
- Use CodePipeline/Jenkins/GitHub Actions
- Validate (cfn-lint), deploy stacks
- Integrate Change Set review

#### Q29. Nested stacks?
Stack inside another stack; reuse/modularize templates (e.g., main stack calls VPC stack, EC2 stack).

#### Q30. Scenario: Automate infra for new projects (VPC, SG, EC2)?
- Modular templates for VPC, SG, EC2
- Combine using nested stacks
- Parameters for customization
- Use StackSets for multi-account

---
