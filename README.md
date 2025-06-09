# MERN Deployment on Azure Kubernetes Service (AKS)

## 📌 Project Overview

This project demonstrates deploying a MERN-based microservices application on Azure Kubernetes Service (AKS). The application used is [SampleMERNwithMicroservices](https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices).

The stack includes:
- React frontend
- Node.js + Express backend
- MongoDB database

---

## 🚀 Deployment Architecture

- Dockerized services pushed to Azure Container Registry (ACR)
- Kubernetes manifests used to deploy services
- Ingress controller used to expose frontend
- MongoDB deployed as a pod inside AKS

---

## 📂 Project Structure  

project-root/  
│
├── kubernetes/  
│   ├── frontend-deployment.yml  
│   ├── backend-deployment.yml  
│   ├── mongo-deployment.yml  
│   ├── service-*.yml  
│   └── ingress.yml  
│
├── docker/  
│   ├── Dockerfile.frontend  
│   ├── Dockerfile.backend  




