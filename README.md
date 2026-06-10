
# GitOps CI/CD Pipeline with Jenkins, Docker, Kubernetes and ArgoCD

## Project Overview

This project demonstrates a complete GitOps-based Continuous Integration and Continuous Deployment (CI/CD) pipeline using:

* Jenkins
* Docker
* GitHub
* Kubernetes
* ArgoCD

The application is automatically built, containerized, pushed to Docker Hub, and deployed to Kubernetes through ArgoCD.

---

## Architecture

Developer → GitHub → Jenkins → Docker Hub → GitHub Manifest Repo → ArgoCD → Kubernetes Cluster

---

## Technologies Used

| Tool       | Purpose                 |
| ---------- | ----------------------- |
| GitHub     | Source Code Management  |
| Jenkins    | CI/CD Pipeline          |
| Docker     | Containerization        |
| Docker Hub | Image Registry          |
| Kubernetes | Container Orchestration |
| ArgoCD     | GitOps Deployment       |

---

## Repository Structure

```text
.
├── app/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── deployment.yaml
├── service.yaml
├── Jenkinsfile
└── README.md
```

---

## Prerequisites

* Docker Installed
* Jenkins Installed
* Kubernetes Cluster Running
* ArgoCD Installed
* Docker Hub Account
* GitHub Personal Access Token

---

## Jenkins Pipeline Stages

### 1. Checkout Code

Jenkins pulls source code from GitHub.

### 2. Build Docker Image

```bash
docker build -t manasabolla/flask-app:${BUILD_NUMBER} .
```

### 3. Push Image to Docker Hub

```bash
docker push manasabolla/flask-app:${BUILD_NUMBER}
```

### 4. Update Deployment Manifest

Jenkins updates image tag inside deployment.yaml.

### 5. Push Changes to GitHub

Updated manifest is pushed to GitHub.

### 6. ArgoCD Sync

ArgoCD detects changes and deploys automatically.

---

# Screenshots

## 1. GitHub Repository

Insert Screenshot Here

Example:

![GitHub Repository](screenshots/github-repo.png)

---

## 2. Jenkins Dashboard

Insert Screenshot Here

![Jenkins Dashboard](screenshots/jenkins-dashboard.png)

---

## 3. Successful Jenkins Build

Insert Screenshot Here

![Jenkins Build Success](screenshots/jenkins-build-success.png)

---

## 4. Docker Hub Image

Insert Screenshot Here

![Docker Hub](screenshots/dockerhub-image.png)

---

## 5. ArgoCD Application

Insert Screenshot Here

![ArgoCD Application](screenshots/argocd-app.png)

---

## 6. Kubernetes Pods

Insert Screenshot Here

![Pods Running](screenshots/k8s-pods.png)

---

## Verification

```bash
kubectl get pods
kubectl get svc
kubectl get deployments
```

Expected Output:

* Pods Running
* Deployment Available
* Service Exposed

---

## Outcome

Successfully implemented a GitOps-based CI/CD pipeline where:

* Jenkins builds Docker images.
* Images are pushed to Docker Hub.
* Deployment manifests are updated automatically.
* ArgoCD synchronizes changes to Kubernetes.
* Application is deployed without manual intervention.

---


DevOps Engineer
AWS | Kubernetes | Jenkins | Docker | ArgoCD | GitOps
