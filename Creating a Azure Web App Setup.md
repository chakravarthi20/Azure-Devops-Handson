# 🚀 Creating a Web App in Azure Portal
Azure App Service enables you to build and host web apps in the programming language of your choice without managing infrastructure. It supports automatic scaling and high availability.

We will now walk through how to create a Web App from the Azure Portal.

### 🧱 Step 1: Navigate to App Services
![image](https://github.com/user-attachments/assets/6bd69e3b-ceef-4616-a1d6-c4d74b36d24a)
Open the Azure Portal: https://portal.azure.com -> In the searchbar, search for App Services -> Click on + Create → Web App 

### 🧾 Step 2: Fill in Basics – Project Details and Instance Settings
On the Basics tab:
Project Details:
- Subscription: Select the appropriate subscription (e.g., Azure for Students).
- Resource Group: Either choose an existing resource group or click Create new.
- Here: chakravarthi-dev_group is created.
- Instance Details: Name: Give a globally unique name.
  Example: chakravarthi-dev → this becomes part of your URL like chakravarthi-dev.azurewebsites.net.
- Publish: Select Code (used for code-based deployments).
- Runtime stack: Select ASP.NET V4.8 (based on the app framework you're using).
- Operating System: Select Windows.
- Region: Choose the closest region (e.g., East US) to reduce latency.
![image](https://github.com/user-attachments/assets/d4919d35-bdb4-4b2b-b0db-91b77b95f328)

### 💵 Step 3: Select Pricing Plan
Screenshot 📸:
Windows Plan: Select or create a new App Service Plan.
Here: ASP-chakravarthidevgroup-ada5 is created.
Pricing Plan: Choose based on budget.
For testing, select Free F1 (Shared infrastructure).
Note: This tier is sufficient for learning/testing purposes but has limited compute and features.
![image](https://github.com/user-attachments/assets/f262e0e3-d35e-45a8-9862-8e1d5324dbd0)

### ✅ Step 4: Review and Create
Once you've completed the basic setup:
- Click Review + Create, After validation passes, click Create.
- Azure will start provisioning your Web App.

### 🔍 Step 5: View Web App Overview
Once deployed, go to the Overview section of the Web App. Here, you can view:
- Default Domain: e.g., chakravarthi-dev.azurewebsites.net
- Resource Group and Location, App Service Plan, Runtime Stack
- Virtual IP Address and Outbound IPs
![image](https://github.com/user-attachments/assets/b6499bd3-db62-4b7d-b957-1a6b561b458a)

✅ Conclusion
At this point, you've successfully created a Web App on Azure using the portal. This app is now ready for:
- CI/CD deployment from Azure DevOps
- Manual deployment using publish profiles or FTP
- Application Insights and monitoring setup

## Next: Deploying to this Web App via Azure DevOps Release Pipeline (Go to - Deploying to Azure Web App using Release Pipelines).
