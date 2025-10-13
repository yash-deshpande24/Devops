# Variables (10/10/25)

Variables store values/data that can be reused throughout the Terraform configuration.

- Code can reuse.

## Datatypes are:
1. **string:**  
   Stores text values.

2. **number:**  
   Stores numeric values.

3. **bool:**  
   Used for logic and conditional statements.  
   Ex: true/false, yes/no

4. **list:**  
   Sequence of values of some type.  
   - List (numbers): `[22, 8]`  
   - List (strings): `["a", "bc"]`

5. **map:**  
   Collection of key-value pairs.

---

# Hardcode → We done previously in main.tf

## Create main.tf file

```hcl
resource "aws_vpc" "net" {
  cidr_block = var.vpc_cidr_block
  tags = {
    Name = "tf-vpc-bs8"
  }
}

resource "aws_subnet" "pub" {
  vpc_id                  = aws_vpc.net.id
  cidr_block              = var.subnet_cidr_block
  map_public_ip_on_launch = var.auto_pub_ip
  tags = {
    Name = "Public-Subnet"
  }
}

resource "aws_internet_gateway" "igw" {
  vpc_id                  = aws_vpc.net.id
  availability_zone       = var.az
  cidr_block              = var.subnet_cidr_block
  map_public_ip_on_launch = var.auto_pub_ip
  tags = {
    Name = "Public-Subnet"
  }
  Name = "Public-Subnet" "igw-tf-vpc"
}
```

---

```hcl
resource "aws_route_table" "rt-pub" {
  vpc_id = aws_vpc.net.id
  tags = {
    Name = "RT-Public"
  }
  route {
    gateway_id = aws_internet_gateway.igw.id
    cidr_block = "0.0.0.0/0"
  }
}

resource "aws_route_table_association" "rta" {
  route_table_id = aws_route_table.rt-pub.id
  subnet_id      = aws_subnet.pub.id
}

resource "aws_security_group" "firewall" {
  name  = "tf-vpc-sg"
  vpc_id = aws_vpc.net.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

---

```hcl
resource "aws_instance" "Bounce" {
  ami               = var.ami_id
  instance_type     = var.ins_type
  key_name          = var.keypair
  vpc_security_group_ids = [aws_security_group.firewall.id]
  subnet_id         = aws_subnet.pub.id
  user_data = <<-EOF
    #!/bin/bash
    sudo yum update -y
    sudo yum install httpd -y
    systemctl start httpd
    systemctl enable httpd
    echo "Hello Terraform" > /var/www/html/index.html
  EOF
  tags = {
    Name = "web-bounce"
  }
}
```

---

# variables.tf

```hcl

variable "vpc_cidr_block" {
  description = "The CIDR block for the VPC."
  type        = string
  default     = "192.168.0.0/16"
}

variable "az" {
  description = "The availability zone to deploy resources into."
  type        = string
  default     = "ap-southeast-1a"
}

variable "sub_cidr_block" {
  description = "The CIDR block for the subnet."
  type        = string
  default     = "192.168.0.0/22"
}

variable "auto_pub_ip" {
  description = "Whether to assign a public IP address automatically."
  type        = bool
  default     = true
}

variable "ami_id" {
  description = "The ID of the AMI to use for the EC2 instance."
  type        = string
  default     = "ami-xxxxxxxxxxxxxxxxx" # Replace with a valid AMI ID
}

variable "inst_type" {
  description = "The instance type for the EC2 instance."
  type        = string
  default     = "t3.micro"
}

variable "key_pair" {
  description = "The name of the key pair to use for the EC2 instance."
  type        = string
  default     = "key2"
}
```
----

# main.tf

```hcl
resource "aws_vpc" "main" {
  cidr_block = var.vpc_cidr_block # Using a variable
}

resource "aws_subnet" "public" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = var.sub_cidr_block # Using a variable
  availability_zone = var.az             # Using a variable
}

---

# terraform.tfvars

vpc_cidr_block = "192.168.0.0/16"
sub_cidr_block = "192.168.0.0/22"
az             = "ap-southeast-1a"
auto_pub_ip    = true
ami_id         = "ami-0c55b159cbfafe1f0" # Replace with a valid AMI ID
inst_type      = "t3.micro"
key_pair       = "tf-key2"

```
---
# outputs.tf

```hcl
output "public_ip" {
  description = "Public IP address of the EC2 instance"
  value       = aws_instance.web.public_ip
}
```
--
# Add this line to your ~/.bashrc or ~/.zshrc file
alias tf='terraform'

###After setting the alias and reloading your shell, you can use tf as a shortcut for terraform:
- tf init - Initialize the Terraform working directory.
- tf validate - Validate the configuration files.
- tf plan - Create an execution plan.
- tf apply - Apply the changes to create or update infrastructure.
- tf output - View the output values from the state file.

---
