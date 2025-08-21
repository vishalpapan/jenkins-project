CI/CD with Docker, SonarQube, Argo CD, and Kubernetes

This project demonstrates how to build and deploy a Java Maven application using Docker, run code quality checks with SonarQube, and manage deployments using Argo CD with Kubernetes manifests.

🚀 Workflow Overview

Code → Java + Maven project stored in GitHub

Build & Package → Docker image creation

Code Quality Check → SonarQube analysis

Push Image → Push Docker image to Docker Hub

Deploy → Use Kubernetes Deployment manifests

Continuous Delivery → Argo CD syncs changes to cluster

🖼️ Architecture

📌 Block diagram placeholder here (upload image)

⚙️ Setup Instructions
1. Prerequisites

Docker installed and running

Kubernetes cluster (Minikube, Kind, or any cloud K8s)

Argo CD installed in the cluster

SonarQube server running

Docker Hub / GitHub access tokens for authentication

2. Build & Push Docker Image
# Build the image
docker build -t <dockerhub-username>/<app-name>:v1 .

# Login to Docker Hub
docker login

# Push the image
docker push <dockerhub-username>/<app-name>:v1

3. Run SonarQube Analysis
mvn clean verify sonar:sonar \
  -Dsonar.projectKey=<project-key> \
  -Dsonar.host.url=http://<sonarqube-url> \
  -Dsonar.login=<sonarqube-token>

4. Kubernetes Deployment Manifests

📂 k8s-manifests/ contains:

deployment.yaml – Defines application Deployment & Pods

service.yaml – Exposes app via ClusterIP/NodePort/LoadBalancer

Apply manifests manually:

kubectl apply -f k8s-manifests/

5. Argo CD Setup

Create a new Argo CD Application:

apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: java-maven-app
  namespace: argocd
spec:
  destination:
    namespace: default
    server: https://kubernetes.default.svc
  project: default
  source:
    repoURL: https://github.com/<your-username>/<repo-name>.git
    path: k8s-manifests
    targetRevision: HEAD
  syncPolicy:
    automated:
      prune: true
      selfHeal: true


Apply it:

kubectl apply -f argocd-application.yaml -n argocd


Argo CD will continuously sync Git changes to the cluster.

✅ Tech Stack

Java + Maven – Build and package app

Docker – Containerize application

SonarQube – Code quality checks

Kubernetes – Deployment & Service manifests

Argo CD – GitOps-based deployment