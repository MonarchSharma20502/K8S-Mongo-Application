# Kubernetes MongoDB Application Deployment on Minikube

A beginner-friendly Kubernetes project demonstrating how to deploy a MongoDB database and Mongo Express UI on a **Minikube** cluster using Kubernetes resources such as **Deployments, Services, Secrets, and ConfigMaps**.

---

## 📖 Project Overview

This project deploys a MongoDB database inside a Kubernetes cluster and provides a web-based management interface using **Mongo Express**.

The project demonstrates:

- Deploying applications using Kubernetes Deployments
- Securely storing database credentials using Secrets
- Managing application configuration using ConfigMaps
- Internal communication using ClusterIP Service
- External access using NodePort Service
- Communication between multiple pods inside Kubernetes

---

## 🏗 Architecture

```
                Browser
                   │
                   ▼
      Mongo Express External Service
              (NodePort)
                   │
                   ▼
          Mongo Express Pod
                   │
          Reads DB URL from ConfigMap
          Reads Credentials from Secret
                   │
                   ▼
      MongoDB Internal Service (ClusterIP)
                   │
                   ▼
              MongoDB Pod
```

---

## Architecture Diagram

> Replace the image path if you rename your screenshot.

![Architecture](images/architecture.png)

---

## Kubernetes Resources Used

| Resource | Purpose |
|----------|----------|
| Deployment | Creates and manages application pods |
| Service (ClusterIP) | Internal communication with MongoDB |
| Service (NodePort) | Exposes Mongo Express outside the cluster |
| Secret | Stores MongoDB username and password |
| ConfigMap | Stores MongoDB service URL |
| Pod | Runs MongoDB and Mongo Express containers |

---

## Project Structure

```
.
├── mongo-secret.yaml
├── mongo-configmap.yaml
├── mongodb-deployment.yaml
├── mongo-express-deployment.yaml
├── README.md
```

---

## Components

### 1. MongoDB

- Runs inside a Kubernetes Deployment
- Stores application data
- Not directly exposed outside the cluster
- Accessible only through the internal Kubernetes service

---

### 2. MongoDB Internal Service

Service Type:

```
ClusterIP
```

Purpose:

- Provides internal networking
- Gives MongoDB a stable DNS name
- Allows Mongo Express to connect without knowing pod IP

Example:

```
mongodb-service:27017
```

---

### 3. Secret

Stores sensitive information like:

- MongoDB Username
- MongoDB Password

Example:

```
MONGO_INITDB_ROOT_USERNAME
MONGO_INITDB_ROOT_PASSWORD
```

Secrets are Base64 encoded before being stored in Kubernetes.

---

### 4. ConfigMap

Stores non-sensitive configuration.

Example:

```
database_url=mongodb-service
```

Mongo Express reads this value to locate MongoDB.

---

### 5. Mongo Express

Mongo Express is a web-based MongoDB administration interface.

It provides:

- Database browsing
- Collection management
- Document editing
- Query execution

Mongo Express obtains:

- Database URL from ConfigMap
- Username & Password from Secret

---

### 6. Mongo Express External Service

Service Type:

```
NodePort
```

Purpose:

Allows users to access Mongo Express from outside the Kubernetes cluster.

Example:

```
http://<Minikube-IP>:30000
```

---

## Deployment Flow

```
User
   │
   ▼
Mongo Express (NodePort Service)
   │
   ▼
Mongo Express Pod
   │
Reads ConfigMap + Secret
   │
   ▼
MongoDB ClusterIP Service
   │
   ▼
MongoDB Pod
```

---

## How to Deploy

### Step 1

Start Minikube

```bash
minikube start
```

---

### Step 2

Create Secret

```bash
kubectl apply -f mongo-secret.yaml
```

---

### Step 3

Create ConfigMap

```bash
kubectl apply -f mongo-configmap.yaml
```

---

### Step 4

Deploy MongoDB

```bash
kubectl apply -f mongodb-deployment.yaml
```

---

### Step 5

Deploy Mongo Express

```bash
kubectl apply -f mongo-express-deployment.yaml
```

---

### Step 6

Verify Resources

```bash
kubectl get all
```

---

### Step 7

Open Mongo Express

```bash
minikube service mongo-express-service
```

or

```bash
kubectl get svc
```

Open the displayed NodePort URL in your browser.

---

## Verify Pods

```bash
kubectl get pods
```

Expected output:

```
mongodb-xxxxxxxxxx-running
mongo-express-xxxxxxxx-running
```

---

## Verify Services

```bash
kubectl get svc
```

Expected:

```
mongodb-service
mongo-express-service
```

---

## Useful Commands

### View Pods

```bash
kubectl get pods
```

### View Services

```bash
kubectl get svc
```

### View Deployments

```bash
kubectl get deployments
```

### Describe Pod

```bash
kubectl describe pod <pod-name>
```

### View Logs

```bash
kubectl logs <pod-name>
```

### Delete Everything

```bash
kubectl delete -f .
```

---

## Key Kubernetes Concepts Demonstrated

- Deployments
- Pods
- ClusterIP Service
- NodePort Service
- Secrets
- ConfigMaps
- Internal Pod Communication
- Kubernetes DNS
- Environment Variables
- Service Discovery

---

## Learning Outcomes

After completing this project, you will understand:

- How Kubernetes Deployments work
- How Services enable communication between pods
- Difference between ClusterIP and NodePort
- Managing sensitive data using Secrets
- Managing configuration using ConfigMaps
- Deploying multi-tier applications on Kubernetes
- Exposing applications outside a Kubernetes cluster

---

## Technologies Used

- Kubernetes
- Minikube
- Docker
- MongoDB
- Mongo Express
- YAML

---

## Future Improvements

- Use Persistent Volumes (PV)
- Use Persistent Volume Claims (PVC)
- Deploy using Helm Charts
- Configure Ingress
- Add TLS
- Add Horizontal Pod Autoscaler (HPA)
- Deploy on Azure Kubernetes Service (AKS)

---

## Author

**Monarch**

Cloud Infrastructure Engineer | Azure | Kubernetes | Docker | DevOps
