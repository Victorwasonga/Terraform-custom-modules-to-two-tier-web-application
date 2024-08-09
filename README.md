## Terraform custom modules to build Two-Tier Web Application Infrastructure

![Terraform Modules](https://github.com/Victorwasonga/Terraform-custom-modules-to-two-tier-web-application/issues/1/terraform-modules.gif)

## Overview

Welcome to the Terraform project for building and managing a two-tier web application infrastructure. In this project, we leverage Infrastructure as Code (IaC) to streamline the deployment and management of resources using Terraform. We utilize reusable custom Terraform modules to efficiently define, provision, and manage our infrastructure.

This approach ensures consistency across different environments, simplifies maintenance, and reduces the potential for errors. By breaking down the infrastructure into modular components, we make it easier to manage and scale as needed.

### Prerequisites

Before you begin, ensure you have the following:

- [Terraform](https://www.terraform.io/downloads.html) installed on your local machine.
- AWS credentials configured on your local machine.

### Project Structure

Here's an overview of the project directory structure:
```bash
.
├── modules
│   ├── alb
│   │   ├── main.tf
│   │   ├── output.tf
│   │   └── variable.tf
│   ├── asg
│   │   ├── config.sh
│   │   ├── main.tf
│   │   └── variables.tf
│   ├── cloudfront
│   │   ├── main.tf
│   │   ├── output.tf
│   │   └── variables.tf
│   ├── key
│   │   ├── client_keys
│   │   ├── client_keys.pub
│   │   ├── main.tf
│   │   └── output.tf
│   ├── nat
│   │   ├── main.tf
│   │   └── variables.tf
│   ├── rds
│   │   ├── main.tf
│   │   └── variable.tf
│   ├── route53
│   │   ├── main.tf
│   │   └── variables.tf
│   ├── security-group
│   │   ├── main.tf
│   │   ├── outputs.tf
│   │   └── variables.tf
│   └── vpc
│       ├── main.tf
│       ├── outputs.tf
│       └── variables.tf
└── root
    ├── backend.tf
    ├── main.tf
    ├── provider.tf
    ├── Readme.md
    ├── variables.tf
    └── variables.tfvars


```

### Backend Configuration

The backend configuration is crucial for storing the Terraform state file remotely, which allows for collaboration and state locking. Below is the configuration for the `backend.tf` file located in the `root/` directory:

```hcl
terraform {
  backend "s3" {
    bucket         = "bucket_name"
    key            = "backend/filename_to_store.tfstate"
    region         = "us-east-1"
    dynamodb_table = "dynamoDB_table name"
  }
}
```

### Setting Up Variables

Let us configure variables.

create a file named `terraform.tfvars` in the 'root' directory. This file will store the values for the variables used in your Terraform configuration.

region = "us-east-1"
project_name = "terraform-project"
vpc_cidr = "10.0.0.0/16"
public_subnet_az1_cidr = "10.0.0.0/24"
public_subnet_az2_cidr = "10.0.1.0/24"
private_app_subnet_az1_cidr = "10.0.2.0/24"
private_app_subnet_az2_cidr = "10.0.3.0/24"
private_data_subnet_az1_cidr = "10.0.4.0/24"
private_data_subnet_az2_cidr = "10.0.5.0/24"
db_username = "vic"
db_password = "victor2011"

### Deploying the Application

Now that we have everything set up, we are ready to deploy our application to the AWS cloud.

1. **Navigate to the Project Directory**:
   ```bash
   cd root
   ```

2. **Plan the Infrastructure Execution**:
   Use the following command to see the execution plan:
   ```bash
   terraform plan
   ```

3. **Apply the Configuration**:
   Finally, run the command below to deploy the application:
   ```bash
   terraform apply
   ```

## Conclusion

This project demonstrates the power of Terraform and reusable modules in creating and managing a two-tier web application infrastructure. By following the steps outlined above, you can easily deploy and manage the infrastructure for your web applications with consistency and reliability.
```


