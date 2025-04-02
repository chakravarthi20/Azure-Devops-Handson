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
