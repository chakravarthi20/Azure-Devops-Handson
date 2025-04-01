# Azure DevOps VM Agent Setup

## What is an Agent Pool?

An Agent Pool is a collection of build and deployment agents in Azure DevOps that are used to run pipelines. Each pipeline needs at least one agent to run jobs like building, testing, or deploying code.

There are two main types of agents:

- 1. Microsoft-Hosted Agents: These are managed by Azure DevOps. Microsoft maintains and updates the VMs with tools and software.

- 2. Self-Hosted Agents : These are hosted by you—either on your own machine or in a VM in Azure. This gives more control and can help reduce costs when you need specific configurations.

## Create Azure Virtual Machine for Agent Pool

### Step 1: Navigate to Azure Virtual Machines

From Azure Portal, go to Virtual Machines and click on + Create > Azure virtual machine.

![image](https://github.com/user-attachments/assets/27124994-c72e-477e-b164-cc4b70b9f389)


### Step 2: Configure Basic VM Settings

- Subscription: Selected Azure for Students (free tier).

- Resource group: Created a new one called agentpool-vm_group to group related resources.

- Virtual machine name: agentpool-vm

- Region: East US (closer region for performance).

- Availability options: Chose No infrastructure redundancy to reduce cost.

- Security type: Standard (sufficient for testing).

- Image: Ubuntu Server 24.04 LTS - x64 Gen2 (lightweight and ideal for Linux agents).

- Architecture: x64 (compatible with agent binaries).

![image](https://github.com/user-attachments/assets/b8007eda-716a-461b-850a-7ab923cd180a)


### Step 3: Administrator Account Setup

- Authentication type: Chose Password for simplicity.

- Username: azureuser

- Password: Set a secure password.

- Inbound ports: Allowed HTTP (80) and SSH (22) for web and terminal access.

![image](https://github.com/user-attachments/assets/87f31784-d4f8-422b-a231-44b1ffe28de4)


Add Agent Pool in Azure DevOps

### Step 4: Navigate to Project Settings > Agent Pools

Go to Azure DevOps → Project → Project Settings → Agent Pools → Click on + New agent pool.

- Pool name: Linux-AG

- Pool type: Self-hosted

- Permissions: Left unchecked (can be adjusted later).

![image](https://github.com/user-attachments/assets/0263295b-16d9-4e4b-89cf-d89e43b6bdc3)

Configure the Agent on VM

### Step 5: SSH into the VM

Copy the Public IP Address from Azure VM dashboard.Open Git Bash:

ssh azureuser@{your-vm-ip}

Enter your password when prompted. You’re now connected to the VM.

### Step 6: Download and Configure Agent

Inside Azure DevOps Agent Pool → Linux-AG → Click New Agent → Select Linux tab:

Run the following:

- mkdir myagent && cd myagent

- tar zxvf ~/Downloads/vsts-agent-linux-x64-<version>.tar.gz

![image](https://github.com/user-attachments/assets/b06cdb6f-fab9-47b0-af95-3b65c58029fe)

- ~/myagent$ ./config.sh

![image](https://github.com/user-attachments/assets/139b7cc4-25d2-4850-893f-1f9cbcb27bd1)

When asked for Server URL, enter: https://dev.azure.com/{yourorganizationname}

When asked for PAT Token, go to User Settings > Personal Access Tokens → + New Token →

![image](https://github.com/user-attachments/assets/0f562470-d632-4c46-964e-9d362b492073)

- Name: Linux-AG

- Scope: Full Access

- Expiration: 30 days

Click Create and Copy the token.

Paste the token in the terminal.


### Step 7: Run the Agent

./run.sh

This command starts the agent and connects it to the Azure DevOps pool.
You should see:

Listening for Jobs

![image](https://github.com/user-attachments/assets/304596fb-005b-4138-84d2-4e482ae465b0)

Final Verification, your agent become online, now you can use in where ever pipeline you want to run

![image](https://github.com/user-attachments/assets/978c2346-db09-4c93-907e-6e63aebcdc3b)


Agent Online Confirmation

Go to Azure DevOps > Agent Pool Linux-AG > Agents tab. You should see your VM listed as Online with status Idle.

(Refer to Screenshot below)



✅ You have successfully set up a self-hosted Linux agent in Azure DevOps!
