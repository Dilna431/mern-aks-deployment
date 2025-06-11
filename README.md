# MERN Application Deployment on Azure Kubernetes Service (AKS)

This document provides a complete guide to deploying the [Sample MERN with Microservices](https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices) application on Azure Kubernetes Service (AKS).

---

## Table of Contents

* [Project Overview](#project-overview)
* [Architecture](#architecture)
* [Prerequisites](#prerequisites)
* [Step-by-Step Deployment](#step-by-step-deployment)

  * [1. Clone the Repository](#1-clone-the-repository)
  * [2. Build and Push Docker Images](#2-build-and-push-docker-images)
  * [3. Create an AKS Cluster](#3-create-an-aks-cluster)
  * [4. Deploy MongoDB](#4-deploy-mongodb)
  * [5. Deploy Backend and Frontend](#5-deploy-backend-and-frontend)
  * [6. Access the Application](#6-access-the-application)
* [Conclusion](#conclusion)

---

## Project Overview

This project demonstrates how to containerize a MERN (MongoDB, Express, React, Node.js) application and deploy it to Azure Kubernetes Service (AKS).

## Architecture

```
[React Frontend] <---> [Node.js Backend] <---> [MongoDB Database]
      |                        |                    |
    Service                Service              Service
      \________________________|_________________/
                         AKS Cluster
```

---

## Prerequisites

* Azure Subscription
* Azure CLI (`az`)
* Docker
* kubectl
* GitHub Account

---

## Step-by-Step Deployment

### 1. Clone the Repository

```bash
git clone https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices.git
cd SampleMERNwithMicroservices
```

### 2. Build and Push Docker Images

```bash
docker build -t <your-dockerhub-username>/mern-backend:latest -f Dockerfiles/Dockerfile.backend .
docker build -t <your-dockerhub-username>/mern-frontend:latest -f Dockerfiles/Dockerfile.frontend .

docker push <your-dockerhub-username>/mern-backend:latest
docker push <your-dockerhub-username>/mern-frontend:latest
```

### 3. Create an AKS Cluster

```bash
az group create --name mern-rg --location eastus
az aks create --resource-group mern-rg --name mern-aks-cluster --node-count 2 --enable-addons monitoring --generate-ssh-keys
az aks get-credentials --resource-group mern-rg --name mern-aks-cluster
```

### 4. Deploy MongoDB

Apply the following manifest:

```bash
kubectl apply -f k8s-manifests/mongo-deployment.yaml
```

### 5. Deploy Backend and Frontend

```bash
kubectl apply -f k8s-manifests/backend-deployment.yaml
kubectl apply -f k8s-manifests/frontend-deployment.yaml
kubectl apply -f k8s-manifests/services.yaml
```

### 6. Access the Application

* Use `kubectl get svc` to find the external IP.
* Open the IP in the browser to verify the frontend.

---


## ✅ Conclusion

You have successfully deployed a full-stack MERN application on AKS. This setup is scalable, cloud-native, and production-ready with Docker and Kubernetes.

---




