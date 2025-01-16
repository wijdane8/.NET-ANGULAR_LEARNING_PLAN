# **.NET & Angular Guide: Week 7 - DevOps & Deployment**

## **🧩 Day 32: Introduction to Kubernetes**

Welcome to Day 32! Building on your knowledge of Docker, today’s focus is on **Kubernetes**, an orchestration platform that manages containerized applications at scale. By the end of this guide, you’ll understand Kubernetes fundamentals and deploy a simple application to a Kubernetes cluster.

---

## **🧩 What is Kubernetes?**

Kubernetes is an open-source platform for automating the deployment, scaling, and management of containerized applications.

### **Key Features of Kubernetes:**
1. **Scalability:** Automatically scale applications up or down based on demand.
2. **Load Balancing:** Distribute traffic evenly across multiple containers.
3. **Self-Healing:** Replace failed containers automatically.
4. **Declarative Configuration:** Manage infrastructure with configuration files.
5. **Multi-Environment Support:** Deploy seamlessly across different cloud providers or on-premises.

---

## **🧩 Kubernetes Architecture**

### **Key Components**
1. **Pod:** The smallest deployable unit in Kubernetes, typically encapsulating a single container.
2. **Node:** A physical or virtual machine that runs pods.
3. **Cluster:** A group of nodes managed by Kubernetes.
4. **Master Node:** Manages the cluster and schedules pods to worker nodes.
5. **Worker Node:** Executes the pods and reports back to the master.
6. **Deployment:** Defines the desired state of your application.

---

## **🧩 Setting Up Kubernetes**

### **Option 1: Minikube (Local Development)**
Minikube allows you to run a Kubernetes cluster locally.

1. **Install Minikube:**
   Download Minikube from [the official site](https://minikube.sigs.k8s.io/docs/).

2. **Start Minikube:**
   ```bash
   minikube start
   ```

3. **Verify Installation:**
   ```bash
   kubectl cluster-info
   ```

### **Option 2: Kubernetes on the Cloud**
Use cloud providers such as AWS, Azure, or Google Cloud Platform to create a managed Kubernetes cluster.

---

## **🧩 Deploying an Application to Kubernetes**

### **Step 1: Write a Deployment YAML File**
Create a `deployment.yaml` file to define your application.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: taskmanager-api
spec:
  replicas: 3
  selector:
    matchLabels:
      app: taskmanager
  template:
    metadata:
      labels:
        app: taskmanager
    spec:
      containers:
      - name: taskmanager-api
        image: taskmanagerapi:latest
        ports:
        - containerPort: 80
```

### **Step 2: Apply the Deployment**
Deploy the application to the Kubernetes cluster.

```bash
kubectl apply -f deployment.yaml
```

### **Step 3: Expose the Application**
Create a service to expose the application to external traffic.

```bash
kubectl expose deployment taskmanager-api --type=LoadBalancer --port=80
```

### **Step 4: Verify the Deployment**
1. Check the pods:
   ```bash
   kubectl get pods
   ```

2. Check the service:
   ```bash
   kubectl get services
   ```

Access the application using the service’s external IP.

---

## **🧩 Practical Labs**

### **Lab 1: Deploy the .NET API to Kubernetes**
**Goal:** Deploy your Dockerized .NET API to a Kubernetes cluster.

🔧 **Tasks:**
1. Write a `deployment.yaml` for the API.
2. Apply the deployment and expose it as a service.
3. Verify the API is accessible.

---

### **Lab 2: Deploy the Angular App to Kubernetes**
**Goal:** Deploy your Dockerized Angular application to the Kubernetes cluster.

🔧 **Tasks:**
1. Write a `deployment.yaml` for the Angular app.
2. Apply the deployment and expose it as a service.
3. Verify the app is accessible.

---

## **🧩 Reflection Questions**
1. How does Kubernetes differ from Docker in terms of orchestration?
2. What advantages do replicas provide in a Kubernetes deployment?
3. How would you handle scaling your application using Kubernetes?

---

🎉 **Congratulations on completing Day 32!** You’ve learned the basics of Kubernetes and deployed your first containerized application to a cluster. Tomorrow, you’ll explore CI/CD pipelines to automate deployment workflows.

