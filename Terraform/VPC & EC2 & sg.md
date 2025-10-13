# AWS VPC & EC2 Terraform Project

## 1. Project Goal
Create a basic AWS network (VPC) with a public subnet, an Internet Gateway, and a Security Group, then launch an EC2 instance into it.

---

## 2. Creating the VPC and Subnet
The VPC is the foundational network container for your resources.

**Code in `main.tf`:**

```hcl
# Create a VPC
resource "aws_vpc" "main" {
  cidr_block = "192.168.0.0/18"
  tags = {
    Name = "tf-vpc-base"
  }
}

# Create a Public Subnet
resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.main.id
  availability_zone       = "ap-southeast-1a"
  cidr_block              = "192.168.0.0/22"
  map_public_ip_on_launch = true  # This makes it a public subnet

  tags = {
    Name = "public-subnet"
  }
}
```

- `aws_vpc`: Defines the overall IP address space (`192.168.0.0/18`).
- `aws_subnet`: Creates a smaller network range within the VPC.
- `map_public_ip_on_launch = true`: Crucial! This automatically assigns a public IP to instances launched in this subnet, making them accessible from the internet.

---

## 3. Creating the Internet Gateway and Route Table
The Internet Gateway allows communication between your VPC and the internet. The Route Table defines where network traffic is directed.

**Code in `main.tf` (continued):**

```hcl
# Create an Internet Gateway
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id
  tags = {
    Name = "igw-public"
  }
}

# Create a Public Route Table
resource "aws_route_table" "rt_public" {
  vpc_id = aws_vpc.main.id

  # This route sends all internet-bound traffic (0.0.0.0/0) to the Internet Gateway
  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }

  tags = {
    Name = "RT-public"
  }
}

# Associate the Public Route Table with the Public Subnet
resource "aws_route_table_association" "public_assoc" {
  route_table_id = aws_route_table.rt_public.id
  subnet_id      = aws_subnet.public.id
}
```

- `aws_route_table`: The key part is the route block that points to the Internet Gateway. This is what makes the subnet "public".
- `aws_route_table_association`: Links the route table to the subnet, enforcing the routing rules.

---

## 4. Creating the Security Group
The Security Group acts as a virtual firewall for your EC2 instance.

**Code in `main.tf` (continued):**

```hcl
resource "aws_security_group" "firewall" {
  name        = "tf-vpc-sg"
  description = "Allow SSH and HTTP traffic"
  vpc_id      = aws_vpc.main.id

  # INGRESS RULES (Inbound Traffic)

  # Rule 1: Allow SSH access (Port 22)
  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"] # WARNING: Allows SSH from ANY IP. Restrict in production.
  }

  # Rule 2: Allow HTTP access (Port 80)
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"] # Allows web traffic from anywhere.
  }

  # EGRESS RULES (Outbound Traffic)

  # Rule 3: Allow ALL outbound traffic
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"          # "-1" means ALL protocols (including ICMP, TCP, UDP, etc.)
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

- **Ingress**: Inbound rules. Allowing SSH (for terminal access) and HTTP (for web traffic).
- **Egress**: Outbound rule. Allows the instance to make requests to anywhere, which is necessary for downloading updates or software.

---

## 5. Launching an EC2 Instance
Now launch a virtual server into the infrastructure you built.

**Code in `main.tf` (continued):**

```hcl
# Create an EC2 Instance
resource "aws_instance" "web" {
  ami                    = "ami-0abcdef1234567890" # Replace with a valid AMI for your region
  instance_type          = "t2.micro"              # Free-tier eligible type
  subnet_id              = aws_subnet.public.id
  vpc_security_group_ids = [aws_security_group.firewall.id]

  tags = {
    Name = "Terraform-Web-Server"
  }
}
```

- `ami`: The Amazon Machine Image (template for the OS). You must find a valid AMI ID for your specific region.
- `subnet_id`: Places the instance in your public subnet.
- `vpc_security_group_ids`: Attaches the firewall rules you created.

---

## 6. Terraform Workflow & Useful Tips

**Basic Commands:**

- `terraform validate` — Checks your code for syntax errors.
- `terraform plan` — Shows a preview of everything that will be created. (Always run this first!)
- `terraform apply` — Creates the actual resources in AWS.
- `terraform destroy` — Deletes all the resources created by this configuration.

**Using an Alias (Shortcut):**

You can create a shortcut for the terraform command.

```bash
# Add this to your ~/.bashrc or ~/.zshrc file
alias tf='terraform'

# Then you can use:
tf validate
tf plan
tf apply
```

**After apply:**
- Check the EC2 section of the AWS Management Console to see your running instance.
- Use the public IP of the instance to try connecting via SSH (if you have the key) or to view it in a web browser if a web server is installed.

---
