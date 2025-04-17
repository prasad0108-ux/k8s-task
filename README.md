# ☸️ Task 5: Deploying a Web App to Kubernetes on Cloud VM

## ✅ Task Objective

Deploy a containerized web application using Kubernetes.  
We used a cloud-based Linux VM (on Azure) to set up Kubernetes with Minikube and host a sample web app using NGINX.

---

## 💻 Environment Setup

- **Platform:** Azure VM (Pay-As-You-Go)
- **OS:** Ubuntu 22.04 LTS
- **Tools Installed:**
  - Docker
  - Minikube
  - kubectl

---

## 🧱 Kubernetes Components Used

We created the following Kubernetes manifests:

### 1. `deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: webapp
  template:
    metadata:
      labels:
        app: webapp
    spec:
      containers:
      - name: webapp
        image: nginx:latest
        ports:
        - containerPort: 80
```

---

### 2. `service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: webapp-service
spec:
  type: NodePort
  selector:
    app: webapp
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
```

---

## ⚙️ Deployment Steps

1. **Launch a VM** on Azure with Ubuntu
2. **Install Docker:**
   ```bash
   sudo apt update && sudo apt install docker.io -y
   sudo usermod -aG docker $USER
   ```
3. **Install Minikube:**
   ```bash
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   sudo install minikube-linux-amd64 /usr/local/bin/minikube
   ```
4. **Start Minikube with Docker driver:**
   ```bash
   minikube start --driver=docker
   ```
5. **Apply Kubernetes configs:**
   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```
6. **Verify everything is running:**
   ```bash
   kubectl get pods
   kubectl get services
   ```
7. **Access the app in browser:**
   Open `http://<your-cloud-VM-public-IP>:30080`  
   (Make sure port `30080` is open in the VM’s NSG/firewall settings.)

---

## 🔍 What You Should See

The default **NGINX welcome page** indicating the app is successfully running inside the Kubernetes cluster.

---

## 📌 Summary

This task demonstrates how to:

- Set up a Kubernetes cluster using Minikube on a cloud VM
- Deploy a simple containerized app using `Deployment` and `Service`
- Access and test the app externally via NodePort

---

✅ **Successfully completed Task 5 using Kubernetes on Azure VM.**
```

---
