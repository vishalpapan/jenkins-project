#  Jenkins CI/CD Pipeline with GitOps

![CI/CD Pipeline](https://img.shields.io/badge/CI%2FCD-Pipeline-brightgreen)
![Jenkins](https://img.shields.io/badge/Jenkins-Latest-blue)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![ArgoCD](https://img.shields.io/badge/ArgoCD-GitOps-orange)
![SonarQube](https://img.shields.io/badge/SonarQube-Code%20Quality-green)

Complete end-to-end CI/CD pipeline for Java Spring Boot application with Jenkins, SonarQube, Docker, and ArgoCD using GitOps methodology.

##  Overview

Automated pipeline that takes your Java code from commit to production:
```
Code Push → Jenkins Build → SonarQube Analysis → Docker Image → ArgoCD Deploy → Kubernetes
```

## Tech Stack

- **CI/CD**: Jenkins with Pipeline-as-Code
- **Code Quality**: SonarQube 
- **Containerization**: Docker & Docker Hub
- **GitOps**: ArgoCD
- **Orchestration**: Kubernetes/Minikube
- **Build**: Maven + Java 17

## Prerequisites

* Java application code hosted on a Git repository
* Jenkins server
* Kubernetes cluster
* ArgoCD
* SonarQube server
* Docker Hub account

##  Pipeline Stages

| Stage | Action | Tool |
|-------|--------|------|
| 1️⃣ **Checkout** | Clone source code from Git | Git Plugin |
| 2️⃣ **Build & Test** | Build Java application using Maven | Maven Integration |
| 3️⃣ **Code Quality** | Run SonarQube analysis | SonarQube Scanner |
| 4️⃣ **Docker Build** | Package application into container | Docker |
| 5️⃣ **Push Image** | Upload image to Docker Hub | Docker Registry |
| 6️⃣ **Update Manifests** | Update Kubernetes deployment files | Git |
| 7️⃣ **GitOps Deploy** | Deploy to production using ArgoCD | ArgoCD |

##  Jenkins Configuration

### Required Jenkins Plugins:
- Git plugin
- Maven Integration plugin
- Pipeline plugin
- Docker Pipeline plugin
- SonarQube Scanner plugin

### Required Credentials:
- `docker-cred`: Docker Hub username/password
- `github`: GitHub personal access token
- `sonarqube`: SonarQube authentication token

##  Pipeline Flow

```groovy
pipeline {
  agent {
    docker {
      image 'maven:3.9.6-eclipse-temurin-17'
      args '--user root -v /var/run/docker.sock:/var/run/docker.sock'
    }
  }
  stages {
    stage('Checkout') { ... }
    stage('Build and Test') { ... }
    stage('Static Code Analysis') { ... }
    stage('Build and Push Docker Image') { ... }
    stage('Update Deployment File') { ... }
  }
}
```

##  How to Use

1. **Configure Jenkins Pipeline**:
   - Create new pipeline job in Jenkins
   - Connect to your Git repository
   - Add required credentials
   
2. **Set up ArgoCD Application**:
   - Point ArgoCD to your Git repository
   - Configure sync policy for automatic deployments
   
3. **Run the Pipeline**:
   - Push code changes to trigger the pipeline
   - Monitor progress through Jenkins UI
   - Verify deployment in ArgoCD dashboard

##  Monitoring

- **Jenkins**: Pipeline execution and build status
- **SonarQube**: Code quality metrics and reports  
- **ArgoCD**: Deployment status and application health
- **Kubernetes**: Application pods and services status

##  Key Features

- ✅ **Automated CI/CD** - Complete automation from code to production
- ✅ **Code Quality Gates** - SonarQube integration for quality assurance
- ✅ **GitOps Deployment** - ArgoCD for declarative deployments
- ✅ **Containerized Builds** - Docker-based pipeline agents
- ✅ **Scalable Architecture** - Production-ready Kubernetes deployment

---
