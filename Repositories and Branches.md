#**📘 Azure DevOps Practice Guide: Creating Repositories and Branches**
This guide walks you through the essential steps of setting up a Git repository and managing branches using Azure DevOps. Perfect for beginners practicing DevOps workflows.

##**🧠 Introduction: What is a Repository and Branch in Azure DevOps?**
Before diving into the steps, let’s understand the key concepts.

###**📦 What is a Repository?**
A repository (repo) in Azure DevOps is a version-controlled storage space for your project’s source code. It uses Git, a distributed version control system, to help teams collaborate and manage changes in code efficiently. Repos in Azure DevOps support:
-	File versioning
-	Collaboration through pull requests
-	History tracking
-	Branching and merging
You can have multiple repositories inside a single Azure DevOps project, each for different applications or modules.

###**🌿 What is a Branch?**
A branch is essentially a copy of your code base where you can safely make changes without affecting the main code. It’s a common Git practice to:
-	Use the main branch for production-ready code
-	Use the develop branch for ongoing development
-	Create feature branches like feature/login to isolate work

________________________________________
###**📂 Step 1: Creating a Repository**
🧭 Navigate to Repos

Go to the left panel and click on Repos > Files. This will take you to the repositories section.
Then from the top dropdown, select or filter existing repositories, or click on New repository to create a fresh one.
 ![image](https://github.com/user-attachments/assets/6498f8c9-8108-41ec-be5a-26a8cc002ece)
________________________________________

###**🛠️ Step 2: Create a New Repository**

Once you click on New repository, you will see a dialog box. Here’s what to do:
-	Repository type: Git (default)
-	Repository name: Enter a meaningful name (e.g., asp-net-webapp)
-	Optionally check Add a README
-	Click Create
 ![image](https://github.com/user-attachments/assets/61b861d5-6883-4afa-a7bf-0ce44cba350c)
________________________________________

###**Step 3:🌿 Creating a New Branch**

To manage branches, click on Branches from the left panel.
You’ll see the list of current branches like main, develop, etc. You can also track changes (ahead/behind), commits, and more here.
 ![image](https://github.com/user-attachments/assets/ce8cefd1-e07b-45e2-9196-34805a6bbbfc)
________________________________________

###**🔧 Step 4: Create a New Branch**

Click the New branch button to open the branch creation form.
-	Name: Choose a branch name (e.g., feature/login)
-	Based on: Select the base branch (develop in this case) – this will be the source of the new branch.
-	You can also link work items if needed.
Click Create when done.
![image](https://github.com/user-attachments/assets/f3a9db7d-4a04-469f-8435-b50f7a90db4c)


Make the develop branch created as Default and main branch as compare branch.
-	Default Branch: This is the branch where all commits will go by default unless specified otherwise. In most Git workflows, develop is used as the default because it represents the active development line.
-	Compare Branch: This is used to compare other branches against. Typically, main is set as the compare branch since it reflects the stable production-ready state.
 ![image](https://github.com/user-attachments/assets/06e0055c-9723-4740-9727-0575baa646a9)


