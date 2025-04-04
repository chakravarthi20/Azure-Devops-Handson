## Terraform Azure Project – Code Explanation & Backend Setup

### 📂 Folder Structure
We have three folders:
- `basic-block`: contains individual services like resource group and storage account.
- `remote-state`: used for backend configuration and re-creating the resource group.
- `resource-group`: used for local testing (also holds state files).

---

### Explanation for the basic code implementation of terraform & creating resource group

```hcl
terraform {                                        # Terraform block defines version & providers needed
  required_version = ">= 1.0.0"                    # Ensures Terraform CLI version is 1.0.0 or higher / in real time try to give exact version
  required_providers {
    azurerm = {                                    # Declares Azure provider / we can use any other like aws
      source  = "hashicorp/azurerm"               # Provider source from Terraform Registry
      version = ">= 2.0"                           # Minimum supported version of provider
    }
  }
}
provider "azurerm" {                               # Provider block for Azure
  features {}                                      # Required block, empty features are fine
}
resource "azurerm_resource_group" "rg" {  # Defines Azure Resource Group named my_demo_rg1
  location = "eastus"                              # Location of the resource group
  name     = "my-demo-rg1"                         # Resource group name
}
```
### Creating storage account through terraform
```hcl
resource "azurerm_storage_account" "devops" {     # Declares an Azure Storage Account resource name
  name                     = "devopschakri"       # Globally unique name of the storage account
  resource_group_name      = azurerm_resource_group.rg.name      # Uses the name of previously created resource group named rg
  location                 = azurerm_resource_group.rg.location   # Inherits location from the rg
  account_tier             = "Standard"           # Storage account tier
  account_replication_type = "LRS"                # Replication type (Locally Redundant Storage)
}
```
![image](https://github.com/user-attachments/assets/2930336a-4c42-4a80-8bf1-9910bd9b2f3d)


**📌 Best Practice:** Always create a separate .tf file for each Azure service to keep configurations modular and maintainable.

## 📚 Theory: Terraform Backend
Terraform backend determines how state is loaded and how an operation such as apply is executed. It supports storing the terraform.tfstate file in a central, remote location.

### 🔧 Types of Backends:
- local: default; stores state on local disk.
- azurerm: stores state in Azure Blob Storage.
- s3: stores state in AWS S3.
- gcs: Google Cloud Storage.
- remote: uses Terraform Cloud.


### 📄Creating backend using terraform 
```hcl
terraform {
  required_version = ">=1.0.0"                    # Minimum Terraform version
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"                # Azure provider source
      version = "4.25.0"                           # Specific version of provider
    }
  }

  backend "azurerm" {                              # Backend block to store tfstate remotely
    resource_group_name  = "dev-rg"                # Previously created resource group
    storage_account_name = "devopschakri"          # Storage account already created
    container_name       = "blob"                  # Manually created container in Azure Portal
    key                  = "dev.terraform.tfstate" # Name of the state file
  }
}
provider "azurerm" {
  features {}
}
resource "azurerm_resource_group" "rg" {          # Recreates the resource group for backend initialization
  name     = "dev-rg"
  location = "eastus"
}
```
![image](https://github.com/user-attachments/assets/786578a9-a8af-40b3-b7fc-cbc96810c37c)

**📝 Note:** The container blob was manually created in the Azure Portal under the storage account devopschakri. This is necessary because Terraform cannot create the container before it reads the backend configuration, so it must exist beforehand.
