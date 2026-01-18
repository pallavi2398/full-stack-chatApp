# Full-Stack Chat App on Kubernetes (KIND)

## 📝 Introduction

This project is a **real-time chat application** demonstrating **full-stack development, containerization, and Kubernetes deployment**.  
It includes:  

- **MongoDB database**  
- **Node.js backend**  
- **React frontend**  

All components are deployed on a **local Kubernetes cluster (KIND)**, showing internal service communication, deployment order, and NodePort access for frontend.

---

## 🔹 Architecture & Workflow

A high-level view of the Kubernetes setup:

yaml
Copy code
      ┌──────────────┐
      │   Frontend   │
      │  React App   │
      │ NodePort:    │
      │ 30007        │
      └─────┬────────┘
            │
            │ HTTP / WebSocket
            ▼
      ┌──────────────┐
      │   Backend    │
      │ Node.js API  │
      │ ClusterIP:   │
      │ 3000         │
      └─────┬────────┘
            │
            │ MongoDB connection
            ▼
      ┌──────────────┐
      │   MongoDB    │
      │ ClusterIP:   │
      │ 27017        │
      └──────────────┘
yaml
Copy code

**Explanation:**  

- **Frontend (NodePort 30007):** Exposed to local browser for user interaction.  
- **Backend (ClusterIP 3000):** Handles business logic, authentication, message storage.  
- **MongoDB (ClusterIP 27017):** Stores persistent chat data; only accessible internally.  

---

## ✨ Features

- Real-time messaging using **Socket.io**  
- JWT-based authentication & authorization  
- Scalable architecture using **Docker containers & Kubernetes**  
- Modern frontend with **React & TailwindCSS**  
- NodePort frontend service for local browser access (`http://localhost:30007`)  

---

## 🛠️ Tech Stack

- **Backend:** Node.js, Express, MongoDB, Socket.io  
- **Frontend:** React, TailwindCSS, Zustand  
- **Containerization:** Docker  
- **Orchestration:** Kubernetes (KIND)  
- **CI/CD (optional):** Jenkins Pipeline  
- **Authentication:** JWT  

---

## 🔧 Prerequisites

- [Docker](https://www.docker.com/get-started)  
- [kubectl](https://kubernetes.io/docs/tasks/tools/)  
- [Kind](https://kind.sigs.k8s.io/)  

---

## 🚀 Deployment on Kubernetes (KIND)

1. Clone your repository:

```bash
git clone https://github.com/<your-github-username>/full-stack-chatApp.git
cd full-stack-chatApp
Create KIND cluster:

bash
Copy code
kind create cluster --name kind-cluster --config k8s-manifests/kind-config.yml
Apply namespace:

bash
Copy code
kubectl apply -f k8s-manifests/namespace.yaml
Deploy MongoDB:

bash
Copy code
kubectl apply -f k8s-manifests/mongo -n chatapp
Deploy Backend:

bash
Copy code
kubectl apply -f k8s-manifests/backend -n chatapp
Deploy Frontend:

bash
Copy code
kubectl apply -f k8s-manifests/frontend -n chatapp
Verify deployment:

bash
Copy code
kubectl get pods -n chatapp
kubectl get svc -n chatapp
Access frontend in browser:

arduino
Copy code
http://localhost:30007
🧑‍💼 CI/CD Pipeline (Optional)
Jenkinsfile included for automated deployment.

Stages:

Clean workspace

Checkout code

Deploy MongoDB → Backend → Frontend

Verify pods and services

Note: Pipeline uses prebuilt Docker Hub images for backend and frontend. Can be extended to build and push images automatically.

🔮 Future Enhancements
Add PersistentVolume / PersistentVolumeClaim for MongoDB

Use Secrets / ConfigMaps for sensitive configuration

Configure Ingress for friendly URLs and HTTPS

Deploy on cloud Kubernetes platforms (AWS, GCP, Azure)

📜 License
MIT License
