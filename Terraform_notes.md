# Terraform Documentation

## Overview
- **Developed by**: Hashicorp
- **Purpose**: Create/provision infrastructure in cloud platforms
- **Type**: IAC software (Infrastructure as Code)
- **Language**: HCL (Hashicorp Configuration Language)
- **Platform Support**: Supports almost all cloud platforms
- **OS Support**: Windows, Linux, and others

## Terraform vs Cloud Formation
- **Cloud Formation**: AWS-only infrastructure creation
- **Terraform**: Multi-cloud platform support

## Installation on Windows

### Steps:
1. Download Terraform for Windows and extract the zip file
2. Set path for `terraform.exe` in System Environment Variables
3. Verify installation:
   ```cmd
   terraform -v
   ```
4. Download and install VS Code IDE from https://code.visualstudio.com/download

## Terraform Architecture
<img width="1357" height="433" alt="Screenshot 2025-10-14 at 6 40 34 PM" src="https://github.com/user-attachments/assets/a443ba00-cb95-437f-98f0-876ed9ffa3ff" />

Terraform uses HCL scripts (`.tf` files) with the following workflow:

```
.tf → init → fmt → validate → plan → apply → destroy
```

### Terraform Commands:
- `terraform init`: Initialize terraform script
- `terraform fmt`: Format script indentation (optional)
- `terraform validate`: Verify script syntax (optional)
- `terraform plan`: Create execution plan
- `terraform apply`: Create actual resources in cloud
- `terraform destroy`: Delete created resources

**Note**: `tfstate` file is created to track resources.

## Terraform AWS Documentation
https://registry.terraform.io/providers/hashicorp/aws/latest/docs

## Creating EC2 Instance

### Script Example:
```hcl
provider "aws" {
    region = "ap-south-1"
    access_key = "AKIATCKAMNKD6R2MPM"
    secret_key = "a4LBcQtYuHjmn/dWZES31sQZAoaZLCIwW9P83"
}

resource "aws_instance" "ashokit_linux_vm" {
    ami = "ami-0e53db6fd757e38c7"
    instance_type = "t2.micro"
    key_name = "awslab"
    security_groups = ["default"]
    tags = {
        Name = "LinuxVM"
    }
}
```

### Execution Commands:
```bash
terraform init
terraform validate
terraform fmt
terraform plan
terraform apply --auto-approve
terraform destroy --auto-approve
```

## Variables in Terraform

### Types:
1. **Input Variables**: Supply values to terraform script
2. **Output Variables**: Get values from terraform script after execution

### Input Variables Example (`input-vars.tf`):
```hcl
variable "ami" {
    description = "Amazon machine image id"
    default = "ami-0e53db6fd757e38c7"
}

variable "instance_type" {
    description = "Represents EC2 instance type"
    default = "t2.micro"
}

variable "key_name" {
    description = "Key pair name"
    default = "awslab"
}
```

### Using Variables in Main Script:
```hcl
resource "aws_instance" "ashokit_ec2_vm" {
    ami = var.ami
    instance_type = var.instance_type
    key_name = var.key_name
    security_groups = ["default"]
    tags = {
        Name = "AIT-Linux-VM"
    }
}
```

### Output Variables Example (`output-vars.tf`):
```hcl
output "ec2_vm_public_ip" {
    value = aws_instance.ashokit_ec2_vm.public_ip
}

output "ec2_private_ip" {
    value = aws_instance.ashokit_ec2_vm.private_ip
}

output "ec2_subnet_id" {
    value = aws_instance.ashokit_ec2_vm.subnet_id
}

output "ec2_complete_info" {
    value = aws_instance.ashokit_ec2_vm
}
```

## Creating Multiple EC2 Instances

### Script Example:
```hcl
locals {
    instances_count = 3
    instances_tags = [
        { Name = "Dev-Server" },
        { Name = "QA-Server" },
        { Name = "UAT-Server" }
    ]
}

resource "aws_instance" "ashokit_ec2_vm" {
    count = local.instances_count
    ami = var.ami
    instance_type = var.instance_type
    key_name = var.key_name
    security_groups = ["default"]
    tags = local.instances_tags[count.index]
}

output "instance_ids" {
    value = aws_instance.ashokit_ec2_vm[*].public_ip
}
```

## Assignments
1. Create S3 Bucket
2. Create RDS Instance
3. Create IAM User
4. Create Custom VPC
5. Create EC2 Instance using Custom VPC

## Terraform Modules

### Structure:
```
01-Project/
├── main.tf
├── inputs.tf
├── outputs.tf
└── modules/
    ├── ec2/
    │   ├── main.tf
    │   ├── inputs.tf
    │   └── outputs.tf
    └── s3/
        ├── main.tf
        ├── inputs.tf
        └── outputs.tf
```

### Project Setup with Modules:

1. Create project directory: `03-App`
2. Create `modules` directory
3. Create `ec2` and `s3` directories inside modules
4. Create terraform scripts in each module directory
5. Create `provider.tf` in root module
6. Create `main.tf` in root module to invoke child modules:

```hcl
module "my_ec2" {
    source = "./modules/ec2"
}

module "my_s3" {
    source = "./modules/s3"
}
```

7. Create `outputs.tf` in root module:

```hcl
output "ait_vm_public_ip" {
    value = module.my_ec2.a1
}

output "ait_vm_private_ip" {
    value = module.my_ec2.a2
}
```

## Project Environments

### Environment Types:
- **DEV**: Development environment
- **SIT/QA**: System Integration Testing
- **UAT**: User Acceptance Testing
- **PILOT**: Pre-Production testing
- **PROD**: Production environment

### Environment-specific Variable Files:
- `inputs-dev.tf`
- `inputs-sit.tf`
- `inputs-uat.tf`
- `inputs-pilot.tf`
- `inputs-prod.tf`

### Execution:
```bash
# For DEV environment
terraform apply --var-file=inputs-dev.tf

# For PROD environment
terraform apply --var-file=inputs-prod.tf
```

## Terraform Workspaces

### Commands:
```bash
terraform workspace show
terraform workspace new dev
terraform workspace new qa
terraform workspace new uat
terraform workspace new prod
terraform workspace list
terraform workspace select dev
```

### Working with Workspaces:

1. Create Terraform project
2. Create `provider.tf` with provider details
3. Create environment-specific variable files:
   - `dev.tfvars`
   - `qa.tfvars`
   - `prod.tfvars`
4. Create main resources script
5. Create outputs variable file
6. Create workspaces:
   ```bash
   terraform workspace new dev
   terraform workspace new qa
   ```
7. Select workspace and apply:
   ```bash
   terraform workspace select dev
   terraform apply --var-file=dev.tfvars
   ```

## Taint and Untaint

### Taint Resource:
```bash
terraform taint aws_instance.vm1
terraform apply --auto-approve
```

### Alternative (Replace):
```bash
terraform apply -replace="aws_instance.vm1"
```

## Summary
1. Infrastructure as Code (IAC)
2. Terraform Introduction
3. Terraform Setup (Windows)
4. Terraform Architecture
5. Terraform Scripts using HCL
6. Variables (Input & Output)
7. Terraform Modules
8. Project Environments
9. Terraform Workspaces
10. Resource Taint or Replace
11. Terraform Vault
