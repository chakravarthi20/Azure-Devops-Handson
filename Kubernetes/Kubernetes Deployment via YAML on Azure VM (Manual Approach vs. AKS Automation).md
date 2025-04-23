### Kubernetes Deployment – What and Why
- Deployment in Kubernetes helps manage and maintain a set of pods.
- You define what your app should look like (image, labels, replica count).
- It ensures the desired number of pod replicas are running.
- It also allows for scaling, rolling updates, and rollback to previous versions.

✅ Use Case: When a pod dies, the deployment creates a new one automatically. If an update fails, you can roll back to a stable version.

### 2. Labels & Selectors
- Labels are key-value pairs attached to K8s objects like pods, helping group or filter them.
- Selectors are used by services/deployments to identify target pods based on those labels.
```
Example:
labels:
  app: app1
  type: frontend
Selector:
matchLabels:
  app: app1
  type: frontend
```
🧠 Think of labels as tags and selectors as filters that find the right pods.

### 3: deployment.yml Explained
Your YAML file defines a Deployment named web-deploy with 4 nginx pods.
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-deploy
spec:
  replicas: 4
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
      - name: nginx
        image: nginx:1.17.0
        ports:
        - containerPort: 80
```
🔍 Key parts:
- replicas: 4 → Launch 4 pods.
- matchLabels → Links deployment to matching pods.
- containerPort: 80 → Port exposed inside the container.

📦 You created this in your VM with:
cat > deploy.yml
kubectl create -f deploy.yml
To update:
kubectl apply -f deploy.yml
![image](https://github.com/user-attachments/assets/c7006086-8790-4b36-ab78-73e3ebfb6fc1)

### 4: svc.yml (Service File) Explained
This exposes your pods to be accessible using NodePort type service.
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
spec:
  type: NodePort
  ports:
  - port: 80
  selector:
    app: nginx-app
```
💡 It:
- Opens a port on the node to route traffic to the correct pod.
- Uses selector to find and forward traffic to matching pods.
Command used:
kubectl apply -f svc.yml
![image](https://github.com/user-attachments/assets/ad8d595e-e544-42b5-9cdb-7edf95b2e14c)

### Pic 5: Azure VM – Port Opening
You manually opened port 30944 (from the NodePort service).

Why?
- Kubernetes NodePort assigns ports in the range 30000–32767.
- To access the nginx service externally, you must open that assigned port in Azure’s NSG (Network Security Group).

You opened 30944 to match the port assigned.
![image](https://github.com/user-attachments/assets/a6e38c41-f245-45e7-b784-3a27bb0020e3)

### Pic 6: Deployment Strategy
Rolling Update (default):
- Gradually replaces old pods with new ones.
- Ensures zero downtime.

Recreate:
- Deletes all old pods first, then creates new pods.
- Causes temporary downtime.

**Use Case:**
- Rolling Update is safe for production.
- Recreate is used for breaking changes or when version conflicts exist.
![image](https://github.com/user-attachments/assets/71e59a08-0ee9-497a-964a-0c1951cfdf8c)

### 🔹7: deployment.yml with Rolling Strategy
```
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxUnavailable: 1
    maxSurge: 1
```
**Explanation:**
- maxUnavailable: 1 → At most 1 pod can be down at any time.
- maxSurge: 1 → At most 1 new pod can be created in addition to current running pods.

🌀 This keeps service available during update.
![image](https://github.com/user-attachments/assets/590f2fd0-85e4-42a3-b95d-0e4b6a2b871f)

### 🔹 8: Taint and Toleration
- Taints repel pods from being scheduled on nodes unless tolerations match.

Used for: Isolating workloads
Running critical workloads only on specific nodes

🛠️ Commands:
kubectl taint nodes --all node-role.kubernetes.io/control-plane:NoSchedule
→ Prevents pods from running on control-plane.

To remove:
kubectl taint nodes --all node-role.kubernetes.io/control-plane-

# ✅Summary:
- ✅ Deployed Kubernetes resources manually using YAML files (deploy.yml, svc.yml) on an Azure VM instead of using AKS.
- 🔄 Implemented rolling update strategy in the deployment to ensure zero downtime during version upgrades.
- 🎯 Used labels and selectors to link deployments and services effectively.
- 🌐 Exposed pods externally via NodePort, configured Azure VM NSG to allow custom port access.
- 🛡️ Applied taints and tolerations to control pod scheduling behavior on specific nodes.
