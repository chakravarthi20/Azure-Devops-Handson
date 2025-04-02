# 🚀 Azure DevOps: Deploying to Azure Web App using Release Pipelines
After creating the Web App in Azure Portal, we now set up a Release Pipeline in Azure DevOps to deploy our application.

### 🧭 Step 1: Go to Releases in Azure DevOps
Navigate to your Azure DevOps project
- On the left panel, click Pipelines → Releases.
- Click + New → New release pipeline.
- A template window opens. Click Empty job as shown.
![image](https://github.com/user-attachments/assets/d0a8eb9c-82fe-4017-94a7-79bd65f3c692)

### 📦 Step 2: Add an Artifact (Build Output)
Artifacts are outputs from build pipelines used in deployments.
- Click Add an artifact.
- Source type: Build
- Project: Your DevOps project (e.g., Testing)
- Source (build pipeline): webapp_build-dev
- Default version: Latest
- Source alias: Leave as is or customize
Click Add to attach the build output to this release.
![image](https://github.com/user-attachments/assets/6ffa71fb-6390-4d77-b96a-494c7012aed4)

### ⚙️ Step 3: Configure Deployment Stage and Tasks
Now configure what the release should do in the stage.
- Click on Tasks (top left next to Pipeline tab).
- Under Agent Job, click + to add a task.
- Search for Azure App Service Deploy and click Add.
![image](https://github.com/user-attachments/assets/d47a123d-8a34-4fc9-a9df-08da302712ae)

### 🔧 Step 4: Fill in App Service Deployment Settings
Fill the form with:
- Connection type: Azure Resource Manager
- Azure subscription: Select your subscription (e.g., Azure for Students Starter)
**Note: To get the Subscription ID, and App service name (You should have the service connection and app service in portal.azure, for that please refer to Create service connection.md)**
- App Service type: Web App on Windows
- App Service name: Choose the app you created earlier (e.g., chakravarthi-dev)
- $(System.DefaultWorkingDirectory)/**/*.zip = This picks the latest .zip build artifact automatically.
![image](https://github.com/user-attachments/assets/143f5447-531b-4364-9df0-00e383c14921)

✅ Click Save once done.

### 🚀 Step 5: Create a New Release
Go back to Releases → webapp-dev
- Click + Create release
- Under Artifacts, select the latest version
- Optionally add a Release description
- Click Create
![image](https://github.com/user-attachments/assets/f656cdb0-c550-427a-a0a5-05883bd93273)

Your release is now created and will begin the deployment process to Azure App Service.

### Step 6: Trigger the Release and Monitor Deployment
Once the release is created, you can manually trigger it.
- Go to the Releases tab.
- Click on the newly created release under Pipeline > Releases.
- Click Deploy or let it run if it's already started.
You’ll see the stage (e.g., Dev) turn green once the deployment is succeeded.
![image](https://github.com/user-attachments/assets/76e1cd73-7a5d-4044-9969-d7125dea2c29)

### Step 7: Confirm the Web App is Running
After successful deployment, open the Azure App Service URL in a browser (e.g., https://chakridevops.azurewebsites.net).
Initially, the web app might show a “waiting for content” page if content isn't fully live yet.
![image](https://github.com/user-attachments/assets/a6102eeb-4f05-46f9-abca-7dc0c1c559bd)


### Step 8: Validate the Web App Output
After a short wait, once your deployment is applied, refresh the app URL again.
- You should now see your ASP.NET Core web application live.
![image](https://github.com/user-attachments/assets/5834427c-4357-49a6-a6c6-3dabc68a76cd)

✅ Summary – What You Learned
- How to deploy an ASP.NET web app to Azure using Azure DevOps release pipelines.
- How to create and configure a Release Pipeline in Azure DevOps with build artifacts and stages.
- How to manually trigger a release and monitor the deployment status.
- How to validate a successful deployment by checking the Azure App Service URL.
- Understanding deployment flow from build to live deployment on Azure App Service.
