## Terraform custom modules to build Two-Tier Web Application Infrastructure

![Uploading Terraform animation4.gif…]()

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
├── module/
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── nat/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── key/
│   │   ├── client_keys
│   │   └── client_keys.pub
├── root/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── backend.tf
└── README.md
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

To configure variables for your infrastructure, create a file named `terraform.tfvars` in the `root/` directory. This file will store the values for the variables used in your Terraform configuration.

### Deploying the Application

Now that we have everything set up, we are ready to deploy our application to the cloud! 🌥️

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

