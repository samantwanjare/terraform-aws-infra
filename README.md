# terraform-aws-infra# 
🏗️ terraform-aws-infra

> Production-ready AWS infrastructure using Terraform — modular, reusable, and fully version-controlled.

---

## 📁 Folder Structure

```
terraform-aws-infra/
├── modules/
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── ec2/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── eks/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── rds/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── s3/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
├── envs/
│   ├── dev/
│   │   ├── main.tf
│   │   └── terraform.tfvars
│   └── prod/
│       ├── main.tf
│       └── terraform.tfvars
├── main.tf
├── variables.tf
├── outputs.tf
└── README.md
```

---

## 🔧 Modules Included

| Module | Description |
|--------|-------------|
| `vpc` | VPC with public/private subnets, NAT Gateway, IGW |
| `ec2` | EC2 instances with security groups and key pairs |
| `eks` | Managed Kubernetes cluster with node groups |
| `rds` | RDS MySQL/PostgreSQL with Multi-AZ support |
| `s3` | S3 buckets with versioning and lifecycle policies |

---

## 🚀 Usage

```bash
# Initialize Terraform
terraform init

# Preview changes
terraform plan -var-file="envs/dev/terraform.tfvars"

# Apply infrastructure
terraform apply -var-file="envs/dev/terraform.tfvars"

# Destroy infrastructure
terraform destroy -var-file="envs/dev/terraform.tfvars"
```

---

## ⚙️ main.tf (VPC Example)

```hcl
module "vpc" {
  source = "./modules/vpc"

  vpc_name        = "prod-vpc"
  vpc_cidr        = "10.0.0.0/16"
  azs             = ["ap-south-1a", "ap-south-1b"]
  public_subnets  = ["10.0.1.0/24", "10.0.2.0/24"]
  private_subnets = ["10.0.10.0/24", "10.0.20.0/24"]

  enable_nat_gateway = true
  single_nat_gateway = false

  tags = {
    Environment = "production"
    ManagedBy   = "terraform"
    Owner       = "devops"
  }
}
```

---

## 📋 Prerequisites

- Terraform >= 1.3.0
- AWS CLI configured with appropriate IAM permissions
- S3 bucket for remote state (recommended)

---

## 🔐 Remote State (Recommended)

```hcl
terraform {
  backend "s3" {
    bucket = "your-terraform-state-bucket"
    key    = "prod/terraform.tfstate"
    region = "ap-south-1"
  }
}
```

---

## 🏷️ Tech Stack

![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazon-aws&logoColor=FF9900)
![EKS](https://img.shields.io/badge/EKS-FF9900?style=flat-square&logo=amazon-eks)

---

> 💡 **Author:** Samant Wanjare | [GitHub](https://github.com/samantwanjare) | [LinkedIn](https://linkedin.com/in/samantwanjare)
