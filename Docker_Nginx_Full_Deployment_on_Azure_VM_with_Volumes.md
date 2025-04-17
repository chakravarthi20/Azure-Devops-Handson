## ➡️ What are Containers?
- Containerization means bundling an app along with its dependencies into a lightweight, isolated unit.
- Containers simplify development, deployment, and management across different environments without worrying about compatibility.

**Benefits of containers:**
- Portability – Move apps easily across systems (local, test, production).
- Agility – Faster development, testing, and release cycles.
- Scalability – Easily scale up or down based on demand.
- Fault tolerance – If one container fails, others still run.

Container runtime engines like Docker, Containerd, CRI-O, Kubernetes CRI make container execution possible.

### ➡️ Why do we need Containers? 
Problem with traditional deployment:
- Compatibility/Dependency issues: Different libraries and versions across environments (dev, QA, prod).
- Long setup time: Setting up app servers (like Apache, MongoDB) manually is time-consuming.
- Environment drift: Configurations differ between development and production, causing issues.
Solution: Containerize everything together (App + Dependencies + Configurations) ensuring consistency everywhere.

### ➡️ Virtual Machine vs Containers
Virtual Machines (VMs):
- Heavyweight (includes Guest OS).
- Takes more disk space (~20-40 GB).
- Slower boot-up.

Containers:
- Lightweight (only app + binaries/libraries, no separate OS).
- Consumes less space (~100MB to 1GB).
- Boots up super fast (seconds).

Example:
- VM Image size = 40GB
- Docker container = 200MB
- Big difference in speed, resource usage, and cost.

### ➡️ What is Docker? 
- Docker is a platform that allows developers to build, package, and deploy applications quickly using containers.
- Docker packages apps into containers that include everything needed to run (libraries, tools, dependencies, network configurations).

Advantages:
- Each microservice (Apache server, MongoDB, Redis) can run in its own isolated container.
- Easy to manage, scale, and troubleshoot.

## 💻 Let’s Start Practical Work
###  Step 1: Create a Virtual Machine 
Before running Docker, we need a Linux VM to install Docker.
In Azure Portal: Create VM → Ubuntu 22.04 → Size: Standard_B1ms (low cost).
Username: devopsdocker (Set some user name) 
Password: (as you set).
Click Review + Create to launch the VM.
![image](https://github.com/user-attachments/assets/37cce7a3-f420-4e75-a7d7-295305af20bd)

### 1️⃣ I connected to VM 
I connected to my Azure VM using SSH from Windows CMD.
After login, you see standard Ubuntu welcome messages showing:
- Disk usage, Number of users, ublic/Private IP addresses

✅ Now I am inside my Linux machine, ready to install Docker.
![image](https://github.com/user-attachments/assets/e5e16eb5-4e26-4ce5-8ae5-1e795cfd2b56)


### 2️⃣ Installed Docker using script file (explaining commands)
Here are the commands I used:
sudo apt update - 	**Updates the Ubuntu package index to latest versions.**
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y	- **Installs packages necessary to download and install from HTTPS repositories.**
curl -fsSL https://download.docker.com/linux/ubuntu/gpg	sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"	- **Adds Docker’s official repository to apt sources list.**
sudo apt update -	**Updates sources list again after adding Docker repository.**
sudo apt install docker-ce -y - **Installs Docker Community Edition.**
```
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
sudo apt install docker-ce -y
```
✅ After these commands, Docker engine is fully installed and ready to use on my VM.

### 3️⃣ Pulled Docker Image 
Docker Image = A lightweight, standalone package that contains everything needed to run a piece of software (code, runtime, libraries, settings).

I ran:
sudo docker pull nginx

After pull: sudo docker images
I verified nginx image is downloaded — Size: 192 MB.
![image](https://github.com/user-attachments/assets/05d7a9d4-c418-4047-9be6-b7f5b9352fc9)

✅ Docker Image = Blueprint (it is NOT running yet — it’s like a template).

### 4️⃣ Deep Commands and Output Explained 
Command	Explanation
sudo docker run -d nginx	**Run nginx container in detached mode (-d) (runs in background).**
sudo docker ps	**Show running containers (Container ID, Status, Ports, Names, etc.).**
sudo docker logs <container_id>	**See real-time logs of the running container (e.g., nginx starting).**
sudo docker inspect <container_id>	**Get detailed low-level information about container (environment, volumes, ports, etc.).**
🧠 Important:
Always use first few digits of container ID (e.g., 97a) — Docker uniquely identifies it.

✅ Output shows nginx container started successfully, listening on port 80 internally.
![image](https://github.com/user-attachments/assets/04e01ba7-b4d4-4134-9c71-c55f5d14b143)


### 5️⃣ Added Inbound Rule (Pic 4)
🎯 Reason why i am adding:
By default, only SSH (port 22) is open.
Since nginx listens on port 80 inside container, and we map it to 8080 externally, we have to allow incoming HTTP traffic on port 8080 to access nginx from browser.
In Azure Portal > VM > Network Settings, I added an Inbound Rule:
Allowed Port 8080 from Any source.
Protocol: TCP
✅ Without this step, you can’t open nginx page from your laptop.
![image](https://github.com/user-attachments/assets/3d193a98-274a-4b27-974b-3e4d52675e06)


### 6️⃣ Stopping & Mapping Container (Pic 5)
Command	Purpose
sudo docker stop <container_id>	**Stop existing container**
sudo docker rm <container_id>	**Remove stopped container**
sudo docker run -d -p 8080:80 nginx	**Re-run nginx with port mapping: Maps VM's port 8080 → Container’s port 80**
🎯 Now when someone hits VM_Public_IP:8080, it goes into container’s port 80 where nginx listens!
![image](https://github.com/user-attachments/assets/3937f5b6-febf-4bd4-bc9f-06e6e5e727f8)

![image](https://github.com/user-attachments/assets/2ee26098-734e-427e-9cb2-5bf574a6f13d)

### 7️⃣ Created and Copied HTML Page (Pic 7 — Right side)
Created file with: **vi index.html**
Wrote simple:
```
<h1>Welcome to docker</h1>
```
Copied HTML file into nginx container's web folder:
sudo docker cp index.html <container_id>:/usr/share/nginx/html
![image](https://github.com/user-attachments/assets/8869b7f9-e898-48d5-b605-bdb698f42c39)

Left side confirmation:
When I opened the VM public IP at port 8080, it showed "Welcome to docker" — meaning my custom page successfully overwritten nginx default page!

✅ At this stage, my nginx is serving my customized content!

### 8️⃣ Persistent Storage using VM Disk (Pic 8)
**Problem:** If container stops or gets deleted, copied files inside container are also deleted!

**Solution:**
Mount VM folder to container.

**Command	Purpose**:
sudo mkdir /opt/vol	**Create a directory /opt/vol on VM.**
sudo mv index.html /opt/vol/	**Move HTML file into /opt/vol.**
sudo docker run -v /opt/vol:/usr/share/nginx/html -p 8080:80 -d nginx	**Mount /opt/vol into container’s /usr/share/nginx/html.**
🎯 So now nginx directly reads files from VM's disk.
Even if container is killed, data remains safe!
![image](https://github.com/user-attachments/assets/53fd40fb-b774-46e0-a82f-9bbe7c96cd17)

### 9️⃣ Container Stop Verification (Pic 9)
Stopped container:
sudo docker stop <container_id>
Checked VM disk:
ls /opt/vol
✅ index.html file is still present!
🎯 This confirms that by using volumes we achieve persistence — container independent storage!

![image](https://github.com/user-attachments/assets/eb9282ab-d308-4834-8679-dcd127f505d4)

### 🔟 Dockerfile Concept Explained (Pic 10)
**Dockerfile Command	Purpose**
FROM	Base image to build from (e.g., .NET Core SDK 3.1).
WORKDIR	Set working directory inside container.
COPY	Copy local files into container.
ENV	Set environment variables.
EXPOSE	Inform Docker which port the app will use.
ENTRYPOINT	Define the app startup command.
✅ With a Dockerfile, you automate all the manual steps (no need to install things manually inside container).

## ✅Summary:
- Learnt what is container and docker
- Connected to VM successfully.
- Installed Docker manually.
- Pulled nginx image.
- Launched nginx container.
- Opened inbound port in Azure.
- Re-ran container mapping VM:8080 → Container:80.
- Customized welcome page.
- Fixed data loss problem using volumes.
