# Ansible Hands-On Guide for Beginners

This guide covers Ansible from a foundational level, using a step-by-step visual walkthrough based on screenshots. We'll explore key components like configuration management, inventory setup, modules, and executing commands on remote nodes.

---

## 📌 What is Configuration Management?

* **Configuration Management** is the process of maintaining systems (hardware/software) in a **desired state**.
* It ensures consistency over time by helping systems remain:

  * Patched
  * Updated
  * Reconfigured

### 🔁 Configuration Lifecycle

**PLAN → IDENTIFY → CONTROL → REPORT**

* **Changes** are:

  * ✅ Managed
  * ✅ Reviewed
  * ✅ Tracked
  * ✅ Audited

### 🛠 Tools Used:

*

---

## ⚙️ Ansible Overview

Ansible is a **configuration management**, **deployment**, and **orchestration** tool.

* It is a **"Push-based"** tool (master node pushes configurations to target nodes).
* Boosts IT productivity through automation.

### 📈 How Ansible Works

* Connects to nodes using SSH
* Uses small programs called **modules**
* Executes modules remotely, then removes them

### 📌 Architecture:

```text
[Playbook]     [Inventory]
     \             /
      \           /
     [Ansible Management Node]
              |
       ssh to multiple hosts
              |
      ┌──────────────┬──────────────┬─────────────┐
   [Host 1 - A] [Host 2 - B] [Host N - B]
```

---

## ☁️ Creating an Ansible Master Node VM
We created a basic virtual machine using Azure with the following specs:

* **VM Name**: ansible-master-node
* **Region**: East US
* **Image**: Ubuntu Server 22.04 LTS - x64 Gen2
* **Size**: Standard\_B2s (2 vCPU, 4 GB RAM)
* **Authentication**: SSH Public Key or Password
![image](https://github.com/user-attachments/assets/80f3dc3d-a5c9-435b-8960-47491bbdd691)

### 🔗 SSH into the VM:
```bash
ssh username@<public-ip>
```

### 📦 Install Ansible:
```bash
sudo apt update
sudo apt install ansible -y
```

---

## 📂 Ansible Inventory

* Inventory defines the managed nodes you automate, with groups so you can run automation tasks on multiple hosts at the same time 
### 🗂 Default Inventory File:

```bash
/etc/ansible/hosts
```

### 🧾 Example Grouped Inventory:

```
[mail]
server3.company.com
server4.company.com

[db]
server5.company.com
server6.company.com

[web]
server7.company.com
server8.company.com
```

### 🔐 Inventory Parameters:

```
ansible_connection = ssh
ansible_port = 22
ansible_user = root
ansible_ssh_pass = <password>
```

* **Linux**: SSH
* **Windows**: PowerShell Remoting

---

## 📌 Writing to Inventory

I edited the default inventory file using:

```bash
vi /etc/ansible/hosts
```

And added this line: which will provide the user name and password for that IP
```
4.227.237.117 ansible_connection=ssh ansible_user=ansible ansible_ssh_pass=Chakri@316998
```
![image](https://github.com/user-attachments/assets/f7bc715c-9247-4b94-98c6-51f33f9962c4)

---

## ✅ Testing Inventory Connection

### 🧪 Ping Test:

```bash
ansible all -m ping
```

**Expected Output:**

```json
"ping": "pong"
```

### 🖥 Shell Command:
![image](https://github.com/user-attachments/assets/d469db87-9558-488e-9586-75fe91accd7a)

```bash
ansible all -m shell -a 'ls'
```
**Lists files on the remote host**

---

## 🗂 Creating Files & Running Commands

### 📁 Create folder and file:

```bash
mkdir test-file
cat > hello.txt
# type content and Ctrl+C
```

### 📂 Confirming File Creation:

```bash
ansible all -m shell -a 'ls'
```
![image](https://github.com/user-attachments/assets/9a113541-afc7-4310-af2b-f89c91fbbd5e)


**Output:**

```
hello.txt
test-file
```

---

## 📝 Creating Files via Ansible Module

We used the `file` module to create a file remotely:

```bash
ansible web -m file -a "dest=/home/devopsmela/abc.txt mode=600 state=touch"
```

- `dest`: file path
- `mode`: permission
- `state=touch`: creates an empty file if not exists

### 📂 Verify File:

```bash
ansible web -m shell -a 'ls -l'
```
![image](https://github.com/user-attachments/assets/e83f2a61-3edd-4896-bb04-a783afde89ef)

**Output:** shows permission, owner, and timestamp

---

## 📦 Installing Packages via Ansible

We used the `apt` module to install Apache:

```bash
ansible web -b -m apt -a "name=apache2 state=present"
```

* `-b`: runs with sudo privileges
* `-m apt`: use apt module
* `-a`: arguments to module
![image](https://github.com/user-attachments/assets/adcc5e1b-b681-4540-ad57-47bc1f2c1a07)

---

## 📝 Summary

* ✅ Understood the basics of configuration management
* ✅ Set up an Ansible master node on Azure VM
* ✅ Installed Ansible and edited inventory file
* ✅ Used modules to ping, execute shell, create files, and install packages
* ✅ Learned syntax and structure for inventory and ad hoc commands

This hands-on session is a perfect start to real-world automation with Ansible. 🚀
