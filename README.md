## Terraform custom modules to provision and deploy a Two-Tier Web App Infrastructure.

   ![Terraform Animations](terraform%20animations.gif)

## Overview
In this project, we will leverage Infrastructure as Code (IaC) to streamline the deployment and management of resources using Terraform. 
Terraform is a popular tool for defining and provisioning infrastructure as a code. It allows you to create, update, and manage cloud resources in a consistent and repeatable manner.

## What Are Terraform Custom Modules?
Terraform modules are containers for multiple resources that are used together. A custom module is a user-defined module that provides reusable components to define infrastructure.
We will leverage reusable custom Terraform modules to efficiently define, provision, and manage our infrastructure.

## Three-tier architecture, 
This is a software design pattern that divides an application into three main parts or tiers:
the client tier
the server tier
and the database tier.
Each tier has specific responsibilities and interacts with each other to provide functionality to end-users as can be seen below.

![2tieranimation](https://github.com/user-attachments/assets/8f6c603e-0335-4be9-af22-bb9205b530ca)

### Prerequisites

Before you begin, ensure you have the following:

- [Terraform](https://www.terraform.io/downloads.html) installed and AWS credentials configured on your local machine.

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

```
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
```

### Deploying the Application

Now that we have everything set up, we are ready to deploy our application to the AWS cloud.

1. **Navigate to the Project Directory**:
   ```bash
   cd root
   ```

2. **Plan the Infrastructure Execution**:
   Use the following command to see the execution plan:

   ```bash
   terraform init
   ```
  ![Screenshot from 2024-08-06 14-46-48](https://github.com/user-attachments/assets/00cce590-107f-467d-9d5a-36a8773ad299)
   
   ```bash
   terraform plan
   ```
  ![Screenshot from 2024-08-09 11-48-02](https://github.com/user-attachments/assets/8a3a7237-b98b-446d-841d-3c654f28e0d5)    
  
4. **Apply the Configuration**:
   Finally, run the command below to deploy the application:
   ```bash
   terraform apply
   ```
![Screenshot from 2024-08-09 11-50-58](https://github.com/user-attachments/assets/d708b42b-d2af-4884-bd11-597cf9d57c98)
![Screenshot from 2024-08-09 12-00-34](https://github.com/user-attachments/assets/eeb93219-a29e-49ea-ad8c-77f44ba7905a)

## Conclusion
This project demonstrates the power of Terraform and reusable modules in creating and managing infrastructure. By following the steps outlined above, you can easily deploy and manage the infrastructure for your web applications with consistency and reliability.
Thanks for reading and stay tuned for more.
```


