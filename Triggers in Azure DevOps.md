# 🔁 Triggers in Azure DevOps
Triggers in Azure DevOps determine when a pipeline should run automatically. These are useful to automate builds, tests, and deployments whenever changes are made to the codebase or at specific intervals.

## 🧠 Types of Triggers
Azure DevOps supports several types of triggers:
- Branch Triggers (Continuous Integration - CI)
- Path Filters
- Scheduled Triggers
- Pipeline Completion Triggers
- Pull Request (PR) Triggers

### 1. Branch Trigger (CI Trigger)
This is the most common trigger that runs the pipeline when there is a commit to a specified branch.

📍How to set it up:

Go to the Pipeline → select the pipeline (e.g., webapp_build-dev) → Click on the Triggers tab.

- Enable Continuous Integration (CI) (✔️ as shown in red circle in the screenshot).

Under Branch filters, you can:

- Include specific branches (e.g., develop) : When you include develop, it means the pipeline runs whenever code is pushed to this branch.

- Exclude branches (e.g., main) : When you exclude main, it prevents the pipeline from running when code is pushed there.

![image](https://github.com/user-attachments/assets/fdeb591b-1491-42d1-8977-5d0092bcfba7)



### 2. Path Filter Trigger
This is used to trigger the pipeline only when specific files or folders are changed in a commit.

📍How to set it up:

Stay in the same Triggers tab.

Scroll to Path filters and click Add.

Type the specific path (e.g., azdevsecops-webapp/azdevsecops-webapp). - This ensures that your pipeline doesn't run for unrelated changes, saving time and resources.

![image](https://github.com/user-attachments/assets/bd648e1b-e5f7-43f3-a602-54917934edc4)



### 3. Scheduled Trigger
This trigger allows you to schedule the pipeline to run at specific times (e.g., every weekday at 4 AM).

📍How to set it up:

Under the Triggers tab, click Add under the "Scheduled" section.

Choose:

Days of the week (Mon–Fri)

Time (e.g., 04:00 UTC)

Branch filters (e.g., include develop)

📌 Use Case: Helpful for daily builds, nightly tests, or time-based automation.
![image](https://github.com/user-attachments/assets/537fedb8-9d7c-473b-bab7-a6823e2fa0e6)



### 4. Pipeline Completion Trigger
This trigger runs your pipeline only after another pipeline completes successfully.

📍How to set it up:

Under the Triggers tab, go to Build Completion → Click + Add.

Select the pipeline to monitor (e.g., agentpool-basic).

Add optional branch filters like develop.

📌 Use Case: Useful when you want to chain pipelines (e.g., build → test → deploy).
![image](https://github.com/user-attachments/assets/ab2f5811-eee6-4745-9db8-cebaf9986bd4)


### 5. Pull Request (PR) Completion Trigger
This trigger runs the pipeline when a pull request is created or updated.

📍How to set it up (YAML based):

Add the following to your YAML:

yaml
Copy
Edit
pr:
  branches:
    include:
      - develop
📌 Use Case: It helps validate changes before merging them into the target branch, ensuring quality control.


