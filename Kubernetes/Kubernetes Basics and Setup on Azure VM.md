# 1. Container Management and Why Kubernetes
Container Management helps in automating the creation, deployment, scaling, and management of containers.
- Tools like Docker, containerd, Cri-O, Kubernetes CRI provide container runtime.
- Benefits include load balancing, deployment automation, auto-scaling, monitoring, rollback/rollout, scheduling.
- As we already learned Docker is great for containerization, but to manage hundreds of containers, orchestration is needed — that’s where Kubernetes comes.

### 2. Kubernetes Overview
Kubernetes is a Container Management (Orchestration) Tool developed by Google (now under CNCF).
- Open source, written in Golang, also called K8s.
**It handles:**
- Automatic Bin-Packing: Allocates containers based on available resources.
- Networking: Manages network communication between Pods.
- Storage: Allows using external storage like AWS EBS, S3, Azure Blob.

### 3. Kubernetes Core Features
Kubernetes ensures:
- Self-Healing: Restart failed containers, reschedule on node failure.
- Automatic Rollbacks and Rollouts: No downtime during deployments.
- Secrets Management: Secure handling of sensitive data like passwords.
- ConfigMaps: Manage application configurations externally from code.

### 4. Kubernetes Architecture
- Control Plane: Manages the cluster (API Server, Controller Manager, Scheduler, etcd database).
- Worker Nodes: Run actual workloads (Kubelet agent, Kube Proxy for networking).
- Communication happens through API Server.
**Control Plane Components:**
- etcd: Key-Value store of all cluster data.
- API Server: Communication hub.
- Controller Manager: Handles controllers like Deployment Controller, Node Controller.
- Scheduler: Decides which Pod runs where.
![image](https://github.com/user-attachments/assets/38cb55c7-cd38-4231-836d-3afc8f36de50)

### 5. Kubernetes Setup Strategy (Minikube vs kubeadm)
**Minikube**: 1 VM (Master + Worker) for development/testing only.
**Kubeadm:** Ideally 2 VMs (Master Node, Worker Node) for Production setup.

Specs: Ubuntu OS, 4GB RAM each VM.
❗ Cost-Saving Trick: For practice, use single VM where both Master and Worker are combined.

### 6. Azure VM Setup
Created an Ubuntu VM (kube-vm) on Azure for Students:
Size: B2s (2 vCPU, 4GB RAM)
OS: Ubuntu 22.04 LTS
Inbound Ports: SSH (22) and HTTP (80) open.
![image](https://github.com/user-attachments/assets/9f7c99c8-dd5c-4587-8744-99fd2bf0b6cb)

### 7. Installing Docker (Container Runtime)
Followed official Docker documentation.
Created a file docker.sh containing:
```
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo ${UBUNTU_CODENAME:-$VERSION_CODENAME}) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
**Then installed Docker components:**
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
✅ Docker installed successfully!

### 8. Installing kubeadm, kubelet, kubectl
Installed Kubernetes components:
```
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.32/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.32/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```
**Why these commands?**
- kubeadm -> Initialize cluster.
- kubelet -> Runs on all nodes, manages pods and containers.
- kubectl -> CLI to interact with Kubernetes cluster.

❗Important: Versions must be consistent across all components.

### 9. Bootstrapping the Cluster
Initialized cluster:
```
sudo kubeadm init
```
**As a regular user (not sudo), set kubeconfig:**
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
✅ Now kubectl get nodes will show master node!

### 10. Installing CNI (Container Network Interface)
Applied CNI plugin:
```
kubectl apply -f https://reweave.azurewebsites.net/k8s/v1.25/net.yaml
```
**CNI plugin is required to enable networking between Pods inside Kubernetes.**
✅ Now cluster is ready to deploy applications!

# ✅ Summary:
# Kubernetes Cluster Setup on Azure VM
This table outlines the core steps to set up a Kubernetes cluster manually on an Azure Virtual Machine using `kubeadm`.

| Step | Action                              | Purpose                                |
|------|-------------------------------------|----------------------------------------|
| 1    | Create Azure VM                     | Host the Kubernetes cluster            |
| 2    | Install Docker                      | Required container runtime             |
| 3    | Install `kubeadm`, `kubelet`, `kubectl` | Kubernetes core tools                 |
| 4    | `kubeadm init`                      | Initialize the Kubernetes master node  |
| 5    | Configure `kubectl`                 | Allow interaction with the cluster     |
| 6    | Install CNI plugin (e.g., Calico, Flannel) | Enable networking between pods      |

