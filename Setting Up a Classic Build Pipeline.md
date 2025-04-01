# ⚙️ Setting Up a Classic Build Pipeline

### Step 1: Navigate to Pipelines
From the Azure DevOps left panel, click on Pipelines.
![image](https://github.com/user-attachments/assets/53ae3a70-213e-4e7a-97ab-8d1a85192317)


### Step 2: Select Source for Pipeline
If you want to use the classic editor instead of YAML, click on "Use the classic editor" (highlighted).
![image](https://github.com/user-attachments/assets/d8d84f7f-94a3-4b9a-b497-eafd18c1960b)


### Step 3: Choose Repo and Branch
You’ll be asked “Where is your code?”
Since our code is in an Azure DevOps Git repo, select Azure Repos Git.
Team Project: Select the Azure DevOps project (e.g., Testing)
Repository: Select your repo (e.g., asp-net-webapp)
Default Branch for Builds: Choose develop if development is ongoing there
![image](https://github.com/user-attachments/assets/b8ace24e-635f-47aa-83b1-8cad4a2be854)


### Step 4: Choose Build Template
You will be asked to choose a template. Since we are building an ASP.NET application, choose the ASP.NET template and click Apply.
![image](https://github.com/user-attachments/assets/8b1d3ad3-795b-45e8-a5f6-5ce3bc96283b)


### Step 5: Define Pipeline Details
Pipeline name: Give a descriptive name like webapp_build-dev
Agent pool: Leave as Azure Pipelines (It is the free version given by microsfot, In next section we will deep dive in agent pool)
Agent specification: Set to windows-2019 (default for .NET builds)
Solution path: Use wildcard for .sln like **/*.sln
Artifact name: Use any names like drop(default) to store build outputs


### Step 6: Agent Job & Demands
In the Agent job section, tasks like NuGet restore, solution build, test, publish symbols, and artifact packaging are listed.
Under Demands, make sure the agent supports:
-msbuild
-visualstudio
-vstest
These ensure your selected agent has the required capabilities to build and test the project.

![image](https://github.com/user-attachments/assets/b03635c1-7215-4eb6-916b-04007fdcdada)


### Step 7: Run the Pipeline
Once the configuration is complete, click Save & Queue to run the build pipeline.
You’ll see logs, job success/failure status, and artifact summary.
![image](https://github.com/user-attachments/assets/0e49467a-906c-4801-8003-0e72bc54af87)

### Step 8: View Published Artifacts
Click on the published artifacts to view contents like .zip or .xml that were generated during the build.
![image](https://github.com/user-attachments/assets/53f5af41-1f92-4bfc-a4ad-efa6c3f9e3b0)
![image](https://github.com/user-attachments/assets/41ecd4b7-e753-4bc5-9eff-8fca80e21293)
