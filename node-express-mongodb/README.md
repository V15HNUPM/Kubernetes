```markdown
# 🚀 Node.js Express MongoDB Kubernetes Application

A full-stack Node.js Express application with MongoDB, containerized with Docker and deployed on Kubernetes.

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)

## 📋 About

This project demonstrates a complete microservices architecture with:
- **Node.js Express** backend API
- **MongoDB** database for data storage
- **Docker** containerization
- **Kubernetes** orchestration
- Multi-service deployment

## 📁 Project Structure

```
node-express-mongodb/
├── k8s-manifests/              # Kubernetes configuration
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── mongo-deployment.yaml
│   ├── mongo-service.yaml
│   ├── app-deployment.yaml
│   └── app-service.yaml
├── Dockerfile                  # Multi-stage Docker build
├── package.json               # Node.js dependencies
├── server.js                  # Express application
└── README.md                  # This file
```

## 🚀 Quick Start

### Prerequisites
- Docker
- Kubernetes cluster (Minikube, Kind, or cloud)
- kubectl

### 1. Build and Push Docker Image
```bash
docker build -t your-username/node-express-mongodb:latest .
docker push your-username/node-express-mongodb:latest
```

### 2. Deploy to Kubernetes
```bash
# Apply all Kubernetes manifests
kubectl apply -f k8s-manifests/namespace.yaml
kubectl apply -f k8s-manifests/configmap.yaml
kubectl apply -f k8s-manifests/mongo-deployment.yaml
kubectl apply -f k8s-manifests/mongo-service.yaml
kubectl apply -f k8s-manifests/app-deployment.yaml
kubectl apply -f k8s-manifests/app-service.yaml
```

### 3. Access the Application
```bash
# Port forward to access the application
kubectl port-forward service/express-app-service 8080:80 -n node-express-mongodb
```

Visit: http://localhost:8080

## 🔧 Kubernetes Architecture

### Services Deployed
- **Express App**: Node.js application running on port 3000
- **MongoDB**: Database service on port 27017
- **Internal Networking**: Services communicate via ClusterIP

### Configuration
- **Namespace**: `node-express-mongodb` for isolation
- **ConfigMap**: Environment variables and configuration
- **Deployments**: Managed pod lifecycle with replicas
- **Services**: Internal service discovery and load balancing

## 📊 Management Commands

```bash
# Check all resources
kubectl get all -n node-express-mongodb

# View application logs
kubectl logs deployment/express-app -n node-express-mongodb -f

# Check MongoDB logs
kubectl logs deployment/mongo -n node-express-mongodb

# Restart deployment
kubectl rollout restart deployment/express-app -n node-express-mongodb

# Delete everything
kubectl delete -f k8s-manifests/ -n node-express-mongodb
```

## 🐳 Docker Details

The application uses an optimized Dockerfile:
- **Node.js 18 Alpine** base image
- **Multi-stage build** for smaller image size
- **Production-ready** configuration

## 🔍 Troubleshooting

### Common Issues
```bash
# Check pod status
kubectl get pods -n node-express-mongodb

# Describe pod for details
kubectl describe pod -n node-express-mongodb

# Check service endpoints
kubectl get endpoints -n node-express-mongodb
```

### Database Connection
Ensure MongoDB connection string in configmap matches your application requirements.


## 📈 Features

- ✅ Containerized microservices
- ✅ Kubernetes orchestration
- ✅ MongoDB persistence
- ✅ Service discovery
- ✅ Load balancing
- ✅ Resource management
- ✅ Production-ready configuration

## 🔗 Source

This project is based on: [https://github.com/bezkoder/node-express-mongodb](https://github.com/bezkoder/node-express-mongodb)

---

**Happy Coding!** 🚀
```
