# 🔁 Pre-deployment and Post-deployment Conditions & Variables
### ✅ Pre-deployment Conditions
Pre-deployment conditions control whether a stage in a release pipeline should proceed to deployment. You can configure:

- **Trigger**: Define when deployment starts (e.g., after release or manually)
- **Approvals**: Add users to manually approve deployment(Enabled with specified users)
- **Artifact Filters**: Trigger deployment based on branch or tags
- **Schedule**: Automatically deploy at a scheduled time (Mon to Fri, 03:00 UTC)

![image](https://github.com/user-attachments/assets/92e080c6-cf1e-4228-a098-b88b7ddff4b4)
![image](https://github.com/user-attachments/assets/64564fcd-c351-451f-af2f-1fd191464523)

### ✅ Post-deployment Conditions
Post-deployment conditions control what happens **after** a deployment completes.
Options include:
- **Post-deployment approvals**: Manual approval to finalize the release
- **Gates**: Automated quality checks or monitoring
- **Auto-redeploy**: Re-deploy if health checks fail or specific conditions are met

![image](https://github.com/user-attachments/assets/01ccadab-e84b-45d3-9998-d6b9e4eded16)

---
## 📦 Variables in Azure Pipelines
### 🔹 What are Variables?
Variables store values used throughout your pipeline configuration. They help reduce repetition and centralize configuration.
There are two types:
1. **Pipeline Variables** – Scoped to pipeline or individual stages
2. **Variable Groups** – A reusable collection of variables
---
### 🔧 1.Pipeline Variables
Consider i have different stages like dev and stage as below 
![image](https://github.com/user-attachments/assets/a3fe8955-4817-4ee6-9d29-5d237091eddf)

You can define variables directly inside the release pipeline:

Variable Name       | Value         | Scope
--------------------|---------------|-------
app-service-name    | devops-dev    | Dev
app-service-name    | devops-stage  | Stage

![image](https://github.com/user-attachments/assets/f4b2566d-32de-4522-b768-137b62fe75e4)

### these can be referenced using syntax like:
$(app-service-name)
Note: Variable starts with $ sign followed by ()
![image](https://github.com/user-attachments/assets/68ee780d-de47-47db-975b-a52e6e323cf3)
### Used in deployment task like:
App Service Name: $(app-service-name)

## 📘 Variable Groups
### ✅ What is a Variable Group?
A variable group is a shared set of variables that can be reused across pipelines and stages.

### 🛠️ Steps to Create a Variable Group:
Go to Pipelines > Library > Click + Variable group
Enter any name (common) and add variables:
In my case to test and show
Name           | Value
---------------|---------------------
env            | dev
env-stage      | qa
server         | dev.devops.in
server-stage   | stage.devops.in
![image](https://github.com/user-attachments/assets/74248db9-19f8-494e-92ab-88dd0aa8b422)

### 🔗 Linking Variable Group
To use the variable group in your release pipeline:
- Go to Variables tab of your pipeline -> Click on Variable groups -> Select Link variable group and choose your group (common)
- Select scope as Release or specific Stages
  
🧱 Example Multi-Stage Release Pipeline
🧩 Stages:
Dev Stage
Uses app-service-name = devops-dev
Stage
Uses app-service-name = devops-stage
![image](https://github.com/user-attachments/assets/dd1c2c4e-b532-4e03-9cfe-9eda8a487144)
Each stage uses scoped variables to deploy to the correct Azure App Service instance.

## 🔑 Summary of What You Learned
- Use pre-deployment and post-deployment conditions
- Implement variables scoped per stage
- Reuse configurations with variable groups
- Successfully deploy to multiple environments (Dev & Stage)

