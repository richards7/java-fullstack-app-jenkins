# Jenkins, Docker & Kubernetes - Full Stack Application Deployment

## Overview

This project demonstrates a simple end-to-end deployment of a three-tier application using **Docker**, **Docker Hub**, **Jenkins**, and **Kubernetes (Minikube)**.

The application consists of:

* **Frontend** – Static web application served using Nginx
* **Backend** – Node.js and Express REST API
* **Database** – MongoDB (Official Docker Image)

The frontend and backend are containerized using Docker, pushed to Docker Hub, and deployed as Kubernetes Pods. Kubernetes Services are used to enable communication between the application components.

---

## Technologies Used

* Jenkins
* Docker
* Docker Hub
* Kubernetes
* Minikube
* Node.js
* Express.js
* Nginx
* MongoDB
* Git & GitHub

---

## Project Architecture

```text
                   User
                     │
                     │
          http://<Minikube-IP>:30080
                     │
                     ▼
            Frontend Service
              (NodePort)
                     │
                     ▼
            Frontend Pod
                     │
                     │ HTTP Request
                     ▼
            Backend Service
             (ClusterIP)
                     │
                     ▼
            Backend Pod
                     │
                     │ MongoDB Connection
                     ▼
            MongoDB Service
             (ClusterIP)
                     │
                     ▼
             MongoDB Pod
```

---

## Project Directory Structure

```text
jenkins-docker-k8s/
│
├── frontend/
│   ├── Dockerfile
│   └── index.html
│
├── backend/
│   ├── Dockerfile
│   ├── package.json
│   └── server.js
│
├── kubernetes/
│   ├── frontend.yaml
│   ├── backend.yaml
│   ├── database.yaml
│   ├── frontend-service.yaml
│   ├── backend-service.yaml
│   └── database-service.yaml
│
├── Jenkinsfile
├── docker-compose.yml
└── README.md
```

---

## Kubernetes Resources

### Pods

* Frontend Pod
* Backend Pod
* MongoDB Pod

### Services

* Frontend Service (NodePort)
* Backend Service (ClusterIP)
* MongoDB Service (ClusterIP)

---

## Why Services Are Used

Pods receive temporary IP addresses. If a Pod is recreated, its IP changes.

Instead of communicating using Pod IP addresses, Kubernetes Services provide a stable network endpoint.

Example:

Frontend communicates with

```text
http://backend-service:5000
```

Backend communicates with

```text
mongodb://mongodb-service:27017
```

The service name remains the same even if the Pod is recreated.

---

## Deployment Steps

### 1. Start Minikube

```bash
minikube start
```

---

### 2. Deploy Pods

```bash
kubectl apply -f kubernetes/frontend.yaml
kubectl apply -f kubernetes/backend.yaml
kubectl apply -f kubernetes/database.yaml
```

---

### 3. Verify Pods

```bash
kubectl get pods
```

Expected output:

```text
NAME                     READY   STATUS
my-frontend-test2-pod    1/1     Running
my-backend-test2-pod     1/1     Running
my-mongodb-test2-pod     1/1     Running
```

---

### 4. Create Services

```bash
kubectl apply -f kubernetes/frontend-service.yaml
kubectl apply -f kubernetes/backend-service.yaml
kubectl apply -f kubernetes/database-service.yaml
```

---

### 5. Verify Services

```bash
kubectl get svc
```

Example:

```text
NAME                 TYPE        PORT(S)
frontend-service     NodePort    80:30080/TCP
backend-service      ClusterIP   5000/TCP
mongodb-service      ClusterIP   27017/TCP
```

---

### 6. Access the Application

Get the Minikube IP:

```bash
minikube ip
```

Open the application in a browser:

```text
http://<Minikube-IP>:30080
```

or simply run:

```bash
minikube service frontend-service
```

---

## Jenkins Pipeline

The Jenkins pipeline performs the following tasks:

* Clone the GitHub repository
* Build Docker images
* Push Docker images to Docker Hub
* Verify successful image creation

The Docker images are then used by Kubernetes to create the application Pods.

---

## Docker Images

| Component | Image                |
| --------- | -------------------- |
| Frontend  | richards7/frontend:4 |
| Backend   | richards7/backend:4  |
| Database  | mongo:7              |

---

## What I Learned

Working on this project helped me understand:

* Creating Docker images
* Publishing images to Docker Hub
* Writing Declarative Jenkins Pipelines
* Creating Kubernetes Pods
* Creating Kubernetes Services
* Service discovery using Kubernetes DNS
* Difference between NodePort and ClusterIP
* Communication between multiple application components
* Troubleshooting image pull and networking issues in Kubernetes

---

## Challenges Faced

Some of the challenges I encountered during development were:

* Docker image pull failures due to incorrect image tags.
* Understanding the difference between Pod IPs and Service names.
* Configuring NodePort and ClusterIP services correctly.
* Debugging Kubernetes resources using `kubectl describe` and `kubectl logs`.
* Connecting the frontend, backend, and database using Kubernetes Services instead of hardcoded IP addresses.

These issues helped me gain practical troubleshooting experience and a better understanding of Kubernetes networking.

---

## Future Improvements

* Replace standalone Pods with Kubernetes Deployments.
* Add Persistent Volumes for MongoDB.
* Configure Ingress for external routing.
* Integrate automatic Kubernetes deployment into the Jenkins pipeline.
* Deploy the application on a managed Kubernetes service such as Amazon EKS.

---

## Author

**Aashish Richard J**

Final Year – Computer Science and Business Systems

Cloud & DevOps Enthusiast
