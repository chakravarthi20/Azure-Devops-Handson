# 🔐 SSH Key Setup for Azure DevOps
### Step 6: Navigate to Project Directory
Open Git Bash and navigate your project folder.
cd desktop
cd adp-09

![image](https://github.com/user-attachments/assets/737a6507-6de9-4bb5-9d94-e3a8ae955b6f)

### Step 7: Generate SSH Key
Run the following command:
ssh-keygen -t rsa-sha2-512
Follow the prompts to save your key and add a passphrase if needed.
![image](https://github.com/user-attachments/assets/fc7102d3-78da-42d6-92b9-60759e7be98d)

### Step 8: Verify Key Files Created
Navigate to your project folder and ensure your key and .pub files were generated.
![image](https://github.com/user-attachments/assets/372b13f0-757b-4276-b958-10ee789d6141)


### Step 9: Open Azure DevOps SSH Settings
Go to Azure DevOps > User Settings > SSH public keys
![image](https://github.com/user-attachments/assets/c7b4808b-8bac-4544-b519-927b3f53a7b5)


### Step 10: Add New SSH Key
Click New Key, give it a name, and paste the contents of your .pub file.
![image](https://github.com/user-attachments/assets/d69072b9-12ab-4dc7-9195-b6033f2aeb31)


### Step 11: Add SSH Key to Agent
Run the following commands:
eval $(ssh-agent -s)
ssh-add /c/Users/YourName/Desktop/ADP-09/test
ssh-add -l
![image](https://github.com/user-attachments/assets/b5a74881-5460-43d6-8c12-7774645d4ba0)

 ________________________________________
### 🔄 Step 12: Cloning Repository with SSH
Clone Your Repo
Use the SSH clone URL from Azure DevOps:
git clone git@ssh.dev.azure.com:v3/ChakravarthiSangoju/Testing/asp-net-webapp
![image](https://github.com/user-attachments/assets/bf0a44fa-57e8-43ce-bccb-23be22543560)

________________________________________
### 📋Step 13: Git Branch Check -  Check Git Status
Navigate into the cloned project and run:
git status
![image](https://github.com/user-attachments/assets/4aeb575c-dc83-45e1-b092-69eb3443c541)

