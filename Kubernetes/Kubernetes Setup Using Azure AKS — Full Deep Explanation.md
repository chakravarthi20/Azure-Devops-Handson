# Basic Concepts: Before Starting
**Pod:** Smallest deployable unit in Kubernetes; it can run one or more containers inside it. Think of it like a "wrapper" around your container.

**Node:** A virtual machine (or physical server) where the Pods run.

**Cluster:** A set of nodes managed together.

**Master Node:** Controls and manages the cluster.

**Worker Node:** Actually runs the application containers (Pods).


### Why Kubernetes?
Docker only runs containers. Kubernetes manages those containers automatically — scaling, self-healing, networking, etc.

## Now starting setup:
###  1 - Create Kubernetes Cluster
We are using Azure Kubernetes Service (AKS), a fully-managed Kubernetes environment.
- Resource Group: You created a new "devops" group – a logical container to group resources.
- Kubernetes Cluster Name: "devopsaks" → Naming your cluster.
- Region: (US) East US → Region closest to you = better latency.
- Preset Configuration: "Dev/Test" → Optimized for small, cheap environments (perfect for learning/testing).
- Kubernetes Version: 1.31.7 (latest stable one Azure offered).
- Authentication and Authorization: Using local accounts + Kubernetes RBAC (Role-Based Access Control).

✅ Summary:
Created a managed Kubernetes Cluster ready for workloads, with minimum resources and FREE plan.
![image](https://github.com/user-attachments/assets/cf5cfa9c-a3f8-434c-8338-ba393497bab4)

### 2 - Node Pool Configuration
- Node Pool Name: "agentpool" → Default system nodes group.
- Mode: "System" → Main node pool to run system critical pods.
- OS SKU: Ubuntu Linux → Most stable for Kubernetes.
- Node Size: Standard D2ps v6 → 2 vCPUs, 8 GB RAM → Decent specs for learning.
- Node Count: 1 → Only one node initially to save cost.
- Max Pods per Node: 30 → Limit on how many Pods each node can run.

✅ Summary:
Setting up the worker node (VM) that will run your Kubernetes workloads.
![image](https://github.com/user-attachments/assets/dca565a4-ee1d-4ed4-bd6e-b7278132a7bf)

### 3 - Azure Kubernetes Services (AKS) Overview
Azure manages your Kubernetes Control Plane.

**Components:**
- Virtual Network: Your cluster gets a network for pod-to-pod communication.
- Ingress: Controls outside access to services in a cluster.
- Managed Control Plane: Azure manages the Master Node for you.
- Nodes and Node Pools: You manage only the nodes running your app pods.

✅ Summary:
AKS simplifies Kubernetes — Azure manages Master node, you just worry about worker nodes and pods.

### 4 - Shell: Getting Cluster Credentials
Commands Explained:
```
az aks get-credentials --resource-group devops --name devopsaks
kubectl get all
kubectl get nodes
kubectl run webapp-nginx --image=nginx
kubectl get pods
```
- az aks get-credentials --resource-group devops --name devopsaks : Fetches cluster credentials and saves them in ~/.kube/config.
- kubectl get all : Shows all running Kubernetes resources (Pods, Services, etc.)
- kubectl get nodes : Lists nodes in the cluster; shows your node ready.
- kubectl run webapp-nginx --image=nginx : Creates a single Pod called webapp-nginx from the official Nginx Docker image.
- kubectl get pods : Lists the created pods, showing "Running".
![image](https://github.com/user-attachments/assets/3930c02c-8df7-4509-87a4-f5aba2e1c678)

✅ Summary:
You authenticated to your AKS cluster and deployed your first Nginx Pod successfully!

### 5- Deployments and Replicas Management
Commands Explained:
```
kubectl create deployment --image=nginx web-deploy --replicas=10
kubectl get pods
kubectl delete pod web-deploy-xxxx
kubectl scale deployment web-deploy --replicas=5
kubectl describe deployment.apps/web-deploy
```
- kubectl create deployment --image=nginx web-deploy --replicas=10 : Creates a Deployment called web-deploy managing 10 Nginx pods automatically.
- kubectl delete pod web-deploy-xxxx : Deletes a Pod → Deployment automatically creates a new one (self-healing).
- kubectl scale deployment web-deploy --replicas=5 : Scales the Deployment to only 5 replicas.
- kubectl describe deployment.apps/web-deploy : Shows detailed description of the deployment, including strategy, number of Pods, and status.

✅ Summary:
You created, deleted, and scaled your application dynamically inside Kubernetes without downtime!

**🛠 Small Replica Architecture (pic)**
Deployment: web-deploy
 ├── Pod: web-deploy-xxx
 ├── Pod: web-deploy-xxx
 ├── Pod: web-deploy-xxx
 ├── Pod: web-deploy-xxx
 └── Pod: web-deploy-xxx
(Each pod contains Nginx container.)
![image](https://github.com/user-attachments/assets/4da94fb5-a044-4f66-8108-de4dc099389e)

### 6 - Kubernetes Services Overview
![image](https://github.com/user-attachments/assets/55368179-8982-4a23-b1e8-4d81618fa569)

- ClusterIP:Default type.
- Internal communication only.
- NodePort: Exposes the service on a static port between 30000-32767 on each Node IP.
- LoadBalancer: Azure automatically provisions an external IP address → easy access over the internet.

✅ Summary:
Services expose your applications inside and outside of the cluster depending on the type selected.

### 7 - Exposing Service + Verifying Output
Commands:
```
kubectl expose deploy web-deploy --port 80 --name=nginx-svc --type=LoadBalancer
kubectl get all
```
--Exposes the web-deploy Deployment to external traffic.
--port 80: Exposes service at HTTP Port 80.
--name=nginx-svc: Names the service.
--type=LoadBalancer: Azure will create a public IP address.
![image](https://github.com/user-attachments/assets/d477f04c-aea6-4b83-8f88-085d1f9dd5aa)

**Now shows your service of type LoadBalancer with an External-IP.**
curl http://<External-IP>
Tests the Nginx web server by directly accessing the external IP address.

✅ Summary:
You successfully exposed your deployed application over the internet and verified it using curl!

# ✅ Final Summary:
- Deployed a Kubernetes Cluster on Azure AKS launched scalable Nginx deployments
- Exposed them to the internet using LoadBalancer
- Practiced scaling and service concepts.
