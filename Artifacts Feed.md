# 📦 Azure Artifacts with Azure DevOps Build Pipeline
This guide documents how to create and configure Azure Artifacts and use them in Azure Pipelines.

---

## 🔧 Step 1: Create a Feed

- Navigate to the **Artifacts** section from the left menu.
- Click on **Create Feed**.
- Provide a **name** for the feed (e.g., `az-devops`).
- Under **Visibility**, choose `Members of ChakravarthiSangoju` to allow organization-wide access.
- Keep **Include packages from common public sources** checked.
- Set **Scope** to `Project: Testing (Recommended)`.
- Click **Create**.
 ![image](https://github.com/user-attachments/assets/4ef3e343-67a3-45ac-a744-d9e6cba5057c)

---

## 🔨 Step 2: Configure the Build Pipeline to Create and Push NuGet Package

- Go to **Pipelines > az-artifacts-build**.
- In the **Tasks** section under Agent Job:
  - Add the **NuGet pack** task.
    - **Command**: `pack`
    - **Path to csproj or nuspec**: `**/*.csproj`
    - **Configuration to package**: `$(BuildConfiguration)`
    - **Package folder**: `$(Build.ArtifactStagingDirectory)`
![image](https://github.com/user-attachments/assets/66643243-5821-40b5-8174-482f91d7d174)

---

## 🚀 Step 3: Push NuGet Package to the Feed

- Add the **NuGet Push** task after `NuGet pack`.
  - **Command**: `push`
  - **Path to NuGet package(s)**: 
    $(Build.ArtifactStagingDirectory)/**/*.nupkg;$(Build.ArtifactStagingDirectory)/**/*.symbols.nupkg
  - **Target feed location**: `This organization/collection`
  - **Target feed**: `az-devops`

![image](https://github.com/user-attachments/assets/25562501-9e6b-45d3-a36c-c2bc8ef55768)

---

## ⚠️ Step 4: Set Permissions to Avoid Build Errors

If you face permission errors while running the pipeline (especially with `NuGet Push`), do the following:

- Navigate to **Artifacts > Feed Settings > Permissions**.
- Assign `Testing Build Service` the role `Feed Publisher (Contributor)`.
![image](https://github.com/user-attachments/assets/5321c946-0963-4f2f-a396-8442986a8fe2)

---

## 🛠️ Step 5: Using Feed in NuGet Restore

- In your build pipeline:
  - Select the **NuGet restore** task.
  - Under **Feeds to use**, choose `Feed(s) I select here`.
  - Pick your feed name (e.g., `az-devops`).
![image](https://github.com/user-attachments/assets/c95a9981-272d-4971-8406-9b8a76bf8ef1)

---

## 💻 Step 6: Use Package in Visual Studio
Once the build pipeline successfully pushes the package:

- Go to your feed (e.g., `azdevsecops-webapp 1.0.0`).
- Copy the installation command:
  ```powershell
  Install-Package azdevsecops-webapp -Version 1.0.0
![image](https://github.com/user-attachments/assets/50f22e48-6e26-42eb-9c84-7949343fbc25)

## ✅ Summary
What you’ve learned:
- How to create and manage Azure Artifacts feeds.
- How to configure build pipelines to pack and push NuGet packages.
- How to assign permissions to avoid push errors.
- How to select the feed for restoring packages in a build.
- How to use private packages inside Visual Studio via NuGet.
