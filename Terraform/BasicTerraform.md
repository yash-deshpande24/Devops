# Day 1: Terraform Notes

## 1. Introduction to Terraform & IaC
Terraform is an Infrastructure as Code (IaC) tool that lets you build, change, and manage your cloud infrastructure from declarations to ensure safety.

**IaC** means managing infrastructure automatically using code, instead of doing it manually.

**Benefits:**
- Saves time, reduces errors.
- Makes it easier for developers to focus on their work.
- Companies use it to save money, lower risks, and respond faster to new opportunities.

---

## 2. Why Do We Use Terraform? Why Is It Important?
This is the core value of Terraform. We use it to solve major problems with manual infrastructure management.

| Why We Use It              | Why It's Important (The Benefit)      |
|----------------------------|---------------------------------------|
| To Automate Manual Tasks   | Saves Time & Reduces Errors:<br>Automating with code is faster and more reliable than manual clicks in a console. It eliminates human error, ensuring the same setup every time. |
| To Manage Infrastructure as Code | Repeatable & Consistent:<br>Your infrastructure setup becomes a code file. It can be re-used to create identical environments for development, testing, and production. |
| To Support Multiple Clouds (Multi-Cloud) | Avoids Vendor Lock-In & Lowers Risk:<br>You can manage AWS, Azure, and GCP with the same tool and similar code. This allows for a flexible, multi-cloud strategy and reduces dependence on a single vendor. |
| To Track Infrastructure State | Clear Visibility & Control:<br>Terraform's state file acts as a "memory" of what it has created. This allows Terraform to know exactly what to update or destroy, preventing configuration drift. |
| To Use a Declarative Language (HCL) | Easier to Read & Write:<br>You define the desired end state ("I need 2 users"), not the step-by-step commands to get there. HCL is more human-readable than JSON or scripts. |

In short, companies use Terraform (IaC) to save money, lower risks, and respond faster to new opportunities.

---

## 3. How Infrastructure as Code Works
Using IaC with Terraform means using code to manage cloud resources (like AWS EC2, S3, etc.) instead of manual configuration.

It makes your infrastructure setup repeatable, consistent, and error-free.

- Terraform was created by HashiCorp in 2014.
- It uses HCL (HashiCorp Configuration Language) or optional JSON.

---

## 4. Initial Setup

1. **Create an empty repository on GitHub.**
2. **Set up a Codespaces environment** (a cloud-based VS Code editor).
3. **Install Terraform in Codespaces:**

```bash
sudo apt update
sudo apt install terraform  # Use official documentation for the latest method
terraform --version         # Verify the installation
```

**API Definition:**  
An Application Programming Interface (API) is a set of defined rules, protocols, and tools that allows different software applications to communicate with each other.

---

## 5. Terraform vs. AWS CloudFormation

| Feature         | Terraform                      | CloudFormation                |
|-----------------|-------------------------------|-------------------------------|
| Cloud Support   | Multi-cloud (AWS, Azure, GCP) | AWS provider support only     |
| Language        | HCL (more human-readable)      | JSON or YAML                  |
| State Management| Uses state files to track resources | Managed internally by AWS  |
| Modules         | Strong support for modules     | Limited module support        |
| Community       | Strong open-source community   | AWS-specific, closed-source   |

**State Management:**  
Terraform uses a state file to remember the infrastructure it created. This file acts as a "memory" for Terraform.

**Terraform Providers:**  
Plugins that allow Terraform to interact with cloud platforms (e.g., AWS, Azure, GCP, IBM).

---

## 6. Configuring the AWS Provider

The provider configuration is written in a file (e.g., `provider.tf`).  
It contains the code to connect to AWS.

**Important:** Never hardcode secret keys directly in your code, especially if you plan to push to GitHub.

**Initial Setup (Not Recommended for GitHub):**

```hcl
provider "aws" {
  region     = "ap-southeast-1"
  access_key = "YOUR_ACCESS_KEY"  # UNSAFE for GitHub
  secret_key = "YOUR_SECRET_KEY"  # UNSAFE for GitHub
}
```

**Recommended Method: Using AWS CLI Profile**

1. Install the AWS CLI.
2. Configure a named profile:

```bash
aws configure --profile "tf-user"
```

3. Reference the profile in your Terraform code:

```hcl
provider "aws" {
  region  = "ap-southeast-1"
  profile = "tf-user"
}
```

---

## 7. Basic Terraform Commands & Workflow

Create a `main.tf` file for your resources.

**Example: Creating IAM Users**

```hcl
resource "aws_iam_user" "user1" {
  name = "Jay"
}

resource "aws_iam_user" "user2" {
  name = "Veezu"
}
```

**Basic Terraform Workflow:**
- `terraform validate`: Checks the code for syntax errors.
- `terraform plan`: Shows a "preview" of what will be created without making any changes. (Always run this first!)
- `terraform apply`: Creates the actual resources in AWS. (Verify users in the IAM console).
- `terraform destroy`: Deletes all the resources managed by the configuration. (Verify deletion in the IAM console).

---
