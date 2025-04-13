# 🧩 What is Database Automation & Why?
Database automation involves automatically managing database deployment, versioning, and integration using CI/CD tools.
- Reduces human errors, ensures consistent deployments, and integrates seamlessly into DevOps pipelines.

### DACPAC vs BACPAC

| Feature                          | DACPAC (Data-Tier Application Package)                                                                 | BACPAC (Backup Package)                                                              |
|----------------------------------|----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| **Content**                      | Contains only the **schema** (no data).                                                                 | Contains both **schema and data** from the database.                                |
| **Primary Use**                  | Used to **move tested schema** from test to production or vice versa.                                   | Used to **import/export** complete database (schema + data).                        |
| **Operations**                   | `EXTRACT`, `DEPLOY`, `REGISTER`, `UNREGISTER`, `UPGRADE`                                                | `EXPORT`, `IMPORT`                                                                  |
| **Support**                      | Supports only **DDL** operations (e.g., `CREATE`, `DROP`, `ALTER`, etc.)                                | Not specific to DDL/DML; it includes all data operations during import/export.      |
| **DML Support**                  | ❌ Does **not** support **DML** (e.g., `INSERT`, `UPDATE`, `DELETE`)                                     | ✅ Supports full database data, including DML operations.                           |
| **File Extension**              | `.dacpac`                                                                                                | `.bacpac`                                                                            |


### 📌 Step 1: Understand the DEMO Flow
This visual shows the 3 key stages:
- Manual Setup – Azure SQL creation, schema deploy, and DACPAC extraction.
- Automation Pipeline Setup – Azure Repo, DACPAC import in Visual Studio, and CI/CD.
- Database Automation - Test – Add new tables/scripts and push changes for auto deployment.

## ⚙️ Step 2: Manual Setup
(Step from: Initial Setup - Manual)
### 2.1 Create SQL Server & Database in Azure**
Navigate to SQL databases → Create new
Configure:
Database: devopsdb
![image](https://github.com/user-attachments/assets/8de41e09-a490-4b13-bc77-613883aa6ac8)

Server: Create new → devopsdbtest
Workload: Development, Storage: Basic
![image](https://github.com/user-attachments/assets/ec88a43e-45b8-4183-84a5-3607801946c2)

### 2.2 To Deploy Table Manually
- Go to SQL Database and click on query editor in left side panel 
Use Query Editor to run:
![image](https://github.com/user-attachments/assets/e5b75bc5-1ced-426a-8012-b02535b292ae)

Note: If you got any error, If login fails in query editor, add your IP in Networking tab of SQL server.
![image](https://github.com/user-attachments/assets/ee518023-5e76-4014-86b1-e5956130dd7b)

Use Query Editor to run:
```
CREATE TABLE Course (...);
INSERT INTO Course VALUES (...);
```
![image](https://github.com/user-attachments/assets/e1f7830e-7ed6-439c-aec9-e84c527756a3)

### 2.3 Extract DACPAC
Use SQL Server Management Studio (SSMS) → Right-click DB → Tasks → Extract Data-tier Application
![image](https://github.com/user-attachments/assets/b110aa48-a41b-44ec-9cd5-a9f4a76dc76a)

## 📁 Step 3: Automation Pipeline Setup
(Step from: Pipeline Setup for Automation)
### 3.1 Create Azure Repo & Clone Locally
Created db-repo in Azure Repos → Cloned via Git
![image](https://github.com/user-attachments/assets/72c468a2-b361-466a-8430-03fd110ccd25)

### 3.2 Create Visual Studio SQL Project & Import DACPAC
In VS
- Created SQL Server database project in Visual Studio.
- Right-click project → Import Data-tier Application.
- Imported .dacpac file, which created the schema and table in the project.
![image](https://github.com/user-attachments/assets/a2435130-e692-4d3d-be65-4cc380974e28)

## 🔧 Step 4: CI/CD Setup with DACPAC
(Step from: Create CI/CD pipelines)
Intially Created a pipeline using classic editor -> .Net Desktop and build and run that pipeline.

### 4.1 CI Build Pipeline Configuration
Created db_build pipeline with steps:
- Build .sln
- Copy .dacpac to artifact directory
- Publish artifact
![image](https://github.com/user-attachments/assets/33c10ab8-b614-4be2-bdbf-e960e35ba47b)

### 4.2 Release Pipeline for DACPAC Deployment
Created db_release pipeline:
- Task: Azure SQL DACPAC Task, 
- Provide the deatils of server, db, login, and .dacpac path
![image](https://github.com/user-attachments/assets/088caf15-8eba-4787-89b0-3226def54fd9)

## 🧪 Step 5: Database Automation - Test
(Step from: Database Automation - Test)

### 5.1 Add a New Table
Added Subject.sql table script in Visual Studio
![image](https://github.com/user-attachments/assets/c694df45-2560-4a59-b4df-106a15572858)

### 5.2 Add SQL Script Folder
Created Script folder → Added Insert_Subject.sql to insert records

### 5.3 Include Scripts in Build Pipeline
Edited Copy Files step to include:
```
**\*.dacpac  
**\*.sql  
```
![image](https://github.com/user-attachments/assets/8cee4913-e512-401e-91ac-b93dad4ca4e8)

### 5.4 Modify Release Pipeline for Script Execution
Cloned the release stage and renamed it for script execution:
Task: Azure SQL Script Task
Provide .sql file path
![image](https://github.com/user-attachments/assets/eaf454bd-9c1a-4336-86d4-27db54efda2d)


The image shows the successful execution of the db_release pipeline in Azure DevOps.
All stages completed with a green checkmark:
- ✅ Initialize job
- ✅ Download artifact from build pipeline
- ✅ Azure SQL DacpacTask – Schema deployment completed
- ✅ Azure SQL Script Task – Insert script executed
- ✅ Finalize job
![image](https://github.com/user-attachments/assets/ab40d260-9018-448b-bd09-7dde1db9f5cd)

## ✅ Overall Summary – What We Implemented:
- Created an Azure SQL Server & Database manually in the Azure portal.
- Extracted a DACPAC from the live DB using SSMS (only schema, no data).
- Created Azure Repos and cloned it locally to develop database automation.
- Imported DACPAC into a Visual Studio SQL Database Project.
- Configured CI Build Pipeline:
- Created CD Release Pipeline:
-- Stage 1: Deploy .dacpac (schema)
-- Stage 2: Deploy .sql (data insert) using SQL Script Task
- Added a new table (Subject) and insert script
- Committed and pushed changes to Git → triggered build and release
- Release pipeline executed successfully, confirming full database automation.


