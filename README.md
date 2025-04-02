# Azure DevOps Hands-On Guide

This repository contains step-by-step hands-on guides for working with **Azure DevOps**, from setting up repositories and pipelines to deploying a .NET application on Azure Web App using release pipelines.

The goal of this repo is to help you quickly understand and apply core Azure DevOps concepts through practical implementation.

---

## 🔧 What’s Covered

1. **Repositories and Branches**
   - What is a repository and branch in Azure DevOps.
   - How to create and manage them.
     
2. **SSH Key Setup for Azure DevOps**
   - Steps to set up SSH access for secure communication.

3. **Setting Up a Classic Build Pipeline**
   - Creating a build pipeline to build your local .NET code.
   - Steps to compile, package, and publish artifacts.

4. **Agent Pool - Azure DevOps VM Agent Setup**
   - How to configure a custom self-hosted agent pool (if needed).

5. **Triggers in Azure DevOps**
   -  What are different types of triggers
   -  How to configure automatic pipeline triggers (e.g., branch commits)

6. **Creating an Azure Web App Setup**
   - How to provision an Azure Web App for hosting your application.
  
7. **Create Service Connection**
   - How to connect Azure DevOps with your Azure subscription securely.
   - Includes federated credentials and workload identity setup.

8. **Deploying to Azure Web App using Release Pipelines**
   - Creating a release pipeline to deploy your build artifacts.
   - Running a release and verifying deployment to Azure Web App.
     
9. **Pre-deployment and Post-deployment Conditions & Variables**
    - What & Use pre-deployment and post-deployment conditions.
    - What are variables & Implement variables scoped per stage.
    - Reuse configurations with variable groups, Successfully deploy to multiple environments (Dev & Stage)
---

## 💡 Notes

- These guides assume you have a basic understanding of Git and Azure.
- Ideal for learners working with .NET applications in Azure DevOps environments.

Feel free to explore each `.md` file in order — they’re designed to be followed as a complete DevOps workflow.

---

## 📂 Folder Structure

Each `.md` file in this repo represents a self-contained hands-on topic. You can follow them sequentially or jump into the part you need.

