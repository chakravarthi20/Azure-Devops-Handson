# ✅ Prerequisites for Terraform Setup with Azure
### 🧰 Step 1: Install Azure CLI
Download Azure CLI from the official site: https://learn.microsoft.com/en-us/cli/azure/install-azure-cli
After installing, verify the version:
az --version
![image](https://github.com/user-attachments/assets/ff4ede18-cc7e-4297-a657-94048c898fd6)

### 🧰 Step 2: Install Visual Studio Code (VS Code)
Download from: https://code.visualstudio.com/
Launch VS Code after installing.

### 🧩 Step 3: Install HashiCorp Terraform Extension in VS Code
- Go to the Extensions tab (🔌 icon)
- Search for "HashiCorp Terraform" and install it.
This extension provides syntax highlighting and autocompletion for Terraform files – making writing .tf scripts easier and error-free.
![image](https://github.com/user-attachments/assets/f496016f-bec3-4309-a932-d727f9d7e8ef)

### 📦 Step 4: Download and Install Terraform
Visit: https://developer.hashicorp.com/terraform/install
Download the Windows AMD64 zip file.
![image](https://github.com/user-attachments/assets/47dc0ea9-c6dc-4a5a-8828-18d3dfd50bd5)

### 🗂 Step 5: Extract and Set Terraform Path
- Create a folder C:\Terraform.
- Unzip the downloaded Terraform file into this folder.


### ⚙️ Step 6: Set Environment Variable (PATH)
Go to: Control Panel > System > Advanced system settings > Environment Variables
Under System Variables, select Path → click Edit → click New → add:
C:\Terraform
![image](https://github.com/user-attachments/assets/58d32855-57db-4912-b3ce-19ba28172a64)

### 🧪 Step 7: Verify Terraform Installation
Open any terminal (Command Prompt, Git Bash, PowerShell).
Run:
terraform --version
![image](https://github.com/user-attachments/assets/345f815d-ea87-4906-805b-8ce6af4bbb1c)

🔐 Step 8: Log in to Azure
From the terminal, navigate to:
- cd C:\Terraform -> az login
It will open a browser to authenticate and show your Azure subscriptions. ✅ As seen in pic 6, you're successfully logged into your Azure account and ready to run Terraform scripts on Azure resources.
![image](https://github.com/user-attachments/assets/0ea6dd80-944e-4fa6-81de-f1d3f4881bd7)

## ✅ You are set to work with Terraform.
