# 💠 Terraform Azure Resource Group Workflow
This guide walks through creating a resource group in Azure using Terraform, following the official Terraform workflow with CLI commands and their purpose — all demonstrated using VS Code and CLI tools.

### 📁 Step 1: Create Project Folder and Terraform File
- Create a folder (e.g., resource-group) and inside it, create a file named resource-group.tf with the following code:

``` #Terraform Settings Block
terraform {
  required_version = ">= 1.0.0"
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm"
      version = ">= 2.0"
    }
  }
}

#Configure the Microsoft Azure Provider
provider "azurerm" {
  features {}
}

#Create Resource Group
resource "azurerm_resource_group" "my_demo_rg1" {
  location = "eastus"
  name     = "my-demo-rg1"
}
```
![image](https://github.com/user-attachments/assets/a5ab5ad9-f983-4d5a-8bc4-8b318961b6d9)

### 🔹 Step 2: Initialize Terraform
**Terraform init**
📝 This initializes the Terraform working directory. It:
- Downloads the necessary provider plugins
- Creates .terraform.lock.hcl file to pin provider versions
![image](https://github.com/user-attachments/assets/2a39138a-7cae-4d02-a5af-d6514934ca58)

### ✅ Step 3: Validate Configuration
**Terraform validate**
- 📝 This checks for syntax or structural errors in your configuration.
- ✅ Output shows: Success! The configuration is valid.
![image](https://github.com/user-attachments/assets/6dcc8762-4847-4784-846e-351bfe7a166b)

### ✨ Step 4: Format Configuration
**Terraform fmt**
- 📝 This formats your Terraform files using standard style.
- Helpful for keeping code consistent and readable.
![image](https://github.com/user-attachments/assets/98787152-2eb6-4203-ada8-fb9a604bbf75)

### 🔍 Step 5: Preview with Plan
**Terraform plan**
- 📝 Shows what Terraform intends to do:
- In this case, it plans to create 1 new resource group (my_demo_rg1)
- Screenshot shows: Plan: 1 to add, 0 to change, 0 to destroy.
![image](https://github.com/user-attachments/assets/d54c8c4c-462a-47bb-b3f8-72655d658873)

### 🚀 Step 6: Apply to Deploy
**Terraform apply**
- 📝 Applies the planned infrastructure.
- Type yes when prompted to confirm.
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
![image](https://github.com/user-attachments/assets/3397f862-050e-4bd7-b873-91f564178bee)

### ❌ Step 7: Destroy Resources
**Terraform destroy**
- 📝 Destroys all resources created by Terraform.
- Type yes to confirm.
- Output confirms: Destroy complete! Resources: 1 destroyed.
![image](https://github.com/user-attachments/assets/a0b79418-fcad-400c-bee1-dff7fac8687a)

### 🔁 Terraform Workflow Summary
| **Step**   | **Command**         | **Description**                            |
|------------|---------------------|--------------------------------------------|
| Write      | `*.tf` files        | Author IaC in HCL format                   |
| Init       | `terraform init`    | Initialize working directory, download providers |
| Validate   | `terraform validate`| Validate syntax and structure              |
| Format     | `terraform fmt`     | Format `.tf` files to standard style       |
| Plan       | `terraform plan`    | Preview changes before applying            |
| Apply      | `terraform apply`   | Provision infrastructure                   |
| Destroy    | `terraform destroy` | Tear down infrastructure                   |
