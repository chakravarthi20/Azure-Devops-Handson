**📘 Azure DevOps Practice Guide: Creating Repositories and Branches**
This guide walks you through the essential steps of setting up a Git repository and managing branches using Azure DevOps. Perfect for beginners practicing DevOps workflows.

**🧠 Introduction: What is a Repository and Branch in Azure DevOps?**
Before diving into the steps, let’s understand the key concepts.

**📦 What is a Repository?**
A repository (repo) in Azure DevOps is a version-controlled storage space for your project’s source code. It uses Git, a distributed version control system, to help teams collaborate and manage changes in code efficiently. Repos in Azure DevOps support:
•	File versioning
•	Collaboration through pull requests
•	History tracking
•	Branching and merging
You can have multiple repositories inside a single Azure DevOps project, each for different applications or modules.

**🌿 What is a Branch?**
A branch is essentially a copy of your code base where you can safely make changes without affecting the main code. It’s a common Git practice to:
•	Use the main branch for production-ready code
•	Use the develop branch for ongoing development
•	Create feature branches like feature/login to isolate work
________________________________________
**📂 Creating a Repository**
🧭 Step 1: Navigate to Repos
 
Go to the left panel and click on Repos > Files. This will take you to the repositories section.
Then from the top dropdown, select or filter existing repositories, or click on New repository to create a fresh one.
________________________________________

**🛠️ Step 2: Create a New Repository**
 
Once you click on New repository, you will see a dialog box. Here’s what to do:
•	Repository type: Git (default)
•	Repository name: Enter a meaningful name (e.g., asp-net-webapp)
•	Optionally check Add a README
•	Click Create

________________________________________

**🌿 Creating a New Branch
🌱 Step 3: Go to Branches**
 
To manage branches, click on Branches from the left panel.
You’ll see the list of current branches like main, develop, etc. You can also track changes (ahead/behind), commits, and more here.
________________________________________

**🔧 Step 4: Create a New Branch**

Click the New branch button to open the branch creation form.
•	Name: Choose a branch name (e.g., feature/login)
•	Based on: Select the base branch (develop in this case) – this will be the source of the new branch.
•	You can also link work items if needed.
Click Create when done.


Make the develop branch created as Default and main branch as compare branch.
•	Default Branch: This is the branch where all commits will go by default unless specified otherwise. In most Git workflows, develop is used as the default because it represents the active development line.
•	Compare Branch: This is used to compare other branches against. Typically, main is set as the compare branch since it reflects the stable production-ready state.
 ![image](https://github.com/user-attachments/assets/06e0055c-9723-4740-9727-0575baa646a9)


