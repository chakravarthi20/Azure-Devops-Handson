# 🛠 How to Create a Service Connection in Azure DevOps
✅ Goal: To establish a secure link between Azure DevOps and Azure Portal (Azure Resource Manager), allowing DevOps pipelines to deploy resources to Azure.

### Step 1: Navigate to Service Connections
You are in the Azure DevOps Portal → Your Project Settings -> Under Pipelines -> click on Service connections.

This opens the existing connections list and the option to create a new one.
![image](https://github.com/user-attachments/assets/79b9ea9d-daf1-42c6-b155-282ef17889e5)

### Step 2: Start Creating New Service Connection
Click "New service connection" on the top right.
- A list of service connection types appeared on the right pane.
- Select Azure Resource Manager (indicated with a tick).
![image](https://github.com/user-attachments/assets/7a3bf0a3-492a-4836-868f-056b12301e9c)

📝 Azure Resource Manager is the correct choice for deploying resources like App Services, VMs, etc., from DevOps.

### Step 3: Filter for Azure Options
Filtered the list by typing azure in the search box to narrow down the connection types.
- Selected Azure Resource Manager again and clicked Next.
  
📌 This prepares the wizard to set up a connection with your Azure subscription.
-  we need some details such as subscription id, tenat id, client id as below.
-  To get all these details, from here we will switch to azure portal
![image](https://github.com/user-attachments/assets/d3aa618d-f54f-4b9d-a657-2f479eccac0c)


### Step 4: Registering App in Azure AD
Now switch to the Azure Portal.
- Go to Azure Active Directory > App registrations.
- Click on "New registration" to create a new app to authenticate your service connection.
🔐 This app acts as a bridge to let Azure DevOps authenticate securely to Azure resources.
![image](https://github.com/user-attachments/assets/a70a031d-aa06-480d-aca9-f33a900b2641)

### Step 5: Filling App Registration Form
- Enter the app name something as az-devops.
- Selected Single tenant (this org only).
- Left the Redirect URI blank (optional).
Click Register to finish.

This registration gives you access to: Client ID, Tenant ID. These will be used to configure the service connection in DevOps.
![image](https://github.com/user-attachments/assets/8b08c800-ee83-4db5-8dbb-001e1653a03f)


### Step 6: Creating a Client Secret
After registration, navigate to Certificates & secrets under the app.
Clicked New client secret, added description and expiry (e.g. 90 days), and clicked Add.

🔑 You now have a secret value (copy it immediately — it's only shown once) to complete the DevOps connection setup.
![image](https://github.com/user-attachments/assets/4f32ffc6-ca5b-4bbe-84ed-ff220b63274b)


## Service Connection Summary
Back in Azure DevOps, after filling in all values (Subscription, Client ID, Tenant ID, Secret), the service connection was created successfully.
Screenshot shows:
![image](https://github.com/user-attachments/assets/55613625-3da6-4dfa-b3ab-f0e93f39c90f)

- Connection name: azure-students-wif-dev
- Type: Azure Resource Manager
- Auth method: Workload identity federation
- Creator: Your name and email
