
# ☕ Simple Java Docker Application

A minimal Java application containerized with Docker and deployed on Kubernetes. This project demonstrates how to package a simple Java application and run it in a Kubernetes cluster.

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)

## 📋 About

This is a simple Java application that:
- Prints a personalized greeting message
- Displays the current date and time
- Demonstrates containerization with Docker
- Shows Kubernetes deployment for batch-style applications

**Sample Output:**
```
Hello, Vishnu! Current date: Tue Sep 30 04:33:16 GMT 2025
```

## 📁 Project Structure

```
simple-java-docker/
├── k8s-manifests/          # Kubernetes configuration files
│   ├── namespace.yaml
│   ├── deployment.yaml
│   └── service.yaml
├── src/
│   └── Main.java          # Java source code
├── Dockerfile             # Multi-stage Docker build
└── README.md              # This file
```

## 🚀 Quick Start

### Prerequisites
- Docker
- Kubernetes cluster (Minikube, Kind, or cloud)
- kubectl

### 1. Build Docker Image
```bash
docker build -t your-username/simple-java:latest .
```

### 2. Push to Container Registry
```bash
docker push your-username/simple-java:latest
```

### 3. Deploy to Kubernetes
```bash
kubectl apply -f k8s-manifests/namespace.yaml
kubectl apply -f k8s-manifests/deployment.yaml
```

### 4. Check Application Output
```bash
kubectl logs -f deployment/simple-java-app -n simple-java
```

## 🔧 Kubernetes Configuration

### Namespace
Isolates the application in the `simple-java` namespace.

### Deployment
- Runs 1 replica of the Java application
- Container stays running after Java execution
- Resource limits configured
- No health checks (batch-style application)

## 📊 Management Commands

```bash
# Check deployment status
kubectl get all -n simple-java

# View application logs
kubectl logs deployment/simple-java-app -n simple-java

# Restart the application
kubectl rollout restart deployment/simple-java-app -n simple-java

# Delete deployment
kubectl delete -f k8s-manifests/ -n simple-java
```

## 🐳 Docker Details

The application uses a multi-stage Docker build:
- Stage 1: JDK for compilation
- Stage 2: JRE for runtime (smaller image)


## 🔗 Source

This project is based on: [https://github.com/LondheShubham153/simple-java-docker](https://github.com/LondheShubham153/simple-java-docker)


**Happy Coding!** ☕
```
