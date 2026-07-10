# Full Stack Application Deployment using Jenkins, Docker, Docker Hub & Kubernetes

## Project Overview

This project demonstrates a simple CI/CD workflow for deploying a three-tier application using Jenkins. The application consists of a frontend, a backend, and a MongoDB database. Jenkins automates the process of cloning the source code, building Docker images, pushing them to Docker Hub, and deploying the application to Kubernetes (Minikube).

The objective of this project is to understand how different DevOps tools work together to automate the software deployment lifecycle.

---

## Tech Stack

* Jenkins
* Docker
* Docker Hub
* Kubernetes (Minikube)
* Node.js (Backend)
* Nginx + HTML (Frontend)
* MongoDB
* Git & GitHub

---

## Project Structure

```
fullstack-app/
│
├── backend/
│   ├── Dockerfile
│   ├── server.js
│   └── package.json
│
├── frontend/
│   ├── Dockerfile
│   └── index.html
│
├── kubernetes/
│   ├── backend-pod.yaml
│   ├── frontend-pod.yaml
│   └── database-pod.yaml
│
├── docker-compose.yml
├── Jenkinsfile
└── README.md
```

---

## Application Architecture

```
Developer
     │
     ▼
GitHub Repository
     │
     ▼
Jenkins Pipeline
     │
     ├── Clone Repository
     ├── Build Docker Images
     ├── Push Images to Docker Hub
     └── Deploy to Kubernetes
                  │
                  ▼
        ┌────────────────────┐
        │     Kubernetes     │
        ├────────────────────┤
        │  Frontend Pod      │
        │  Backend Pod       │
        │  MongoDB Pod       │
        └────────────────────┘
```

---

## Jenkins Pipeline Workflow

The Jenkins pipeline performs the following tasks:

1. Clones the source code from GitHub.
2. Builds Docker images for the frontend and backend.
3. Pushes the images to Docker Hub.
4. Pulls the images from Docker Hub into Kubernetes.
5. Deploys the frontend, backend, and database pods.
6. Verifies that the application is running successfully.

---

## Docker Images

The following Docker images are used:

* Frontend Image
* Backend Image
* MongoDB Official Image

The frontend and backend images are stored in Docker Hub and pulled by Kubernetes during deployment.

---

## Kubernetes Deployment

The application is deployed as three separate pods:

* Frontend Pod
* Backend Pod
* Database Pod

After creating the pods, Kubernetes downloads the required images from Docker Hub and starts the containers automatically.

Useful commands:

```bash
kubectl apply -f backend-pod.yaml
kubectl apply -f frontend-pod.yaml
kubectl apply -f database-pod.yaml
```

To verify:

```bash
kubectl get pods
```

To view pod details:

```bash
kubectl describe pod <pod-name>
```

---

## Jenkins Pipeline Stages

* Clone Repository
* Build Docker Images
* Push Images to Docker Hub
* Deploy Application
* Verify Deployment

---

## Prerequisites

Before running this project, make sure the following are installed:

* Git
* Docker
* Jenkins
* Minikube
* kubectl
* Docker Hub Account

---

## How to Run the Project

### Step 1

Clone the repository.

```bash
git clone <repository-url>
```

### Step 2

Configure Docker Hub credentials in Jenkins.

### Step 3

Run the Jenkins pipeline.

### Step 4

Push the Docker images to Docker Hub.

### Step 5

Deploy the pods using Kubernetes.

```bash
kubectl apply -f backend-pod.yaml
kubectl apply -f frontend-pod.yaml
kubectl apply -f database-pod.yaml
```

### Step 6

Verify the deployment.

```bash
kubectl get pods
```

---

## Challenges Faced

During the implementation of this project, I encountered a few issues that helped me understand the deployment process better.

* Docker images were initially pushed without the correct tag.
* Kubernetes returned an `ImagePullBackOff` error because it was trying to pull the `latest` tag while the images were pushed with a different tag.
* The container ports for the frontend and backend were initially configured incorrectly.
* Jenkins required proper Docker Hub credentials for pushing images successfully.

Resolving these issues provided practical experience in debugging containerized applications and Kubernetes deployments.

---

## Learning Outcomes

After completing this project, I gained hands-on experience with:

* Writing Declarative Jenkins Pipelines
* Building Docker images
* Managing Docker Hub repositories
* Deploying applications on Kubernetes
* Understanding Pod creation and image pulling
* Troubleshooting deployment issues
* Integrating multiple DevOps tools into a complete CI/CD workflow

---

## Future Improvements

* Deploy the application using Kubernetes Deployments and Services instead of standalone Pods.
* Add LoadBalancer or Ingress support.
* Integrate automated testing into the Jenkins pipeline.
* Add image vulnerability scanning.
* Deploy the application to a cloud Kubernetes cluster such as Amazon EKS or Google Kubernetes Engine.

---

## Author

**Aashish Richard J**

Final Year Student

Cloud & DevOps Enthusiast
