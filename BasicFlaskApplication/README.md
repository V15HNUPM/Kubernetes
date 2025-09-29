
# 🚀 Flask Application with Kubernetes Deployment

A comprehensive guide to containerizing a Flask application and deploying it to Kubernetes with production-ready configurations including persistent storage, environment management, and network access.

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

## 📋 Project Overview

This project demonstrates a complete DevOps workflow for deploying a Flask application to Kubernetes, covering:

- ✅ **Containerization** with Docker
- ✅ **Image Management** with Docker Hub
- ✅ **Kubernetes Deployment** with YAML manifests
- ✅ **Persistent Storage** for SQLite database
- ✅ **Environment Configuration** with ConfigMaps
- ✅ **Network Configuration** with Services & Ingress
- ✅ **Production-Ready** settings

## 🏗️ Architecture

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   Docker Image  │───▶│  Kubernetes      │───▶│  Flask App      │
│   on Docker Hub │    │  Cluster         │    │  Running        │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                              │
                     ┌────────┴────────┐
                     │  Persistent     │
                     │  Storage (PVC)  │
                     └─────────────────┘
```

## 🛠️ Prerequisites

- **Docker** installed and running
- **Kubernetes** cluster (Minikube, Kind, or cloud cluster)
- **kubectl** configured
- **Docker Hub** account

## 📁 Project Structure

```bash
BasicFlaskApplication/
├── k8s-manifests/
│   ├── namespace.yaml          # Environment isolation
│   ├── configmap.yaml          # Application configuration
│   ├── persistentvolumeclaim.yaml # Database storage
│   ├── deployment.yaml         # Flask app deployment
│   ├── service.yaml           # Internal networking
│   └── ingress.yaml           # External access (optional)
├── website/
│   ├── __init__.py            # Flask application factory
│   ├── models.py              # Database models
│   └── views.py               # Application routes
├── Dockerfile                 # Container definition
├── requirements.txt           # Python dependencies
└── main.py                   # Application entry point
```

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/ASHISHKUMAR2411/BasicFlaskApplication
cd BasicFlaskApplication
```

### 2. Build and Push Docker Image

```bash
# Build the Docker image
docker build -t <your-dockerhub-username>/flask-app:latest .

# Push to Docker Hub
docker push <your-dockerhub-username>/flask-app:latest
```

> **💡 Pro Tip:** Always use specific version tags for production deployments.

### 3. Update Image Reference

Edit `deployment.yaml` to use your Docker Hub image:

```yaml
containers:
- name: flask-app
  image: <your-dockerhub-username>/flask-app:latest  # Update this line
```

### 4. Deploy to Kubernetes

Apply the Kubernetes manifests in order:

```bash
# Create namespace
kubectl apply -f k8s-manifests/namespace.yaml

# Apply configuration
kubectl apply -f k8s-manifests/configmap.yaml

# Create persistent storage
kubectl apply -f k8s-manifests/persistentvolumeclaim.yaml

# Deploy the application
kubectl apply -f k8s-manifests/deployment.yaml

# Expose the service
kubectl apply -f k8s-manifests/service.yaml

# Optional: Set up ingress
kubectl apply -f k8s-manifests/ingress.yaml
```

### 5. Verify Deployment

```bash
# Check all resources
kubectl get all -n flask-app

# Monitor application logs
kubectl logs deployment/flask-app -n flask-app -f

# Check persistent volume
kubectl get pvc -n flask-app
```

## 🌐 Access the Application

### Method 1: Port Forwarding (Development)

```bash
kubectl port-forward deployment/flask-app 5000:5000 -n flask-app
```
Access at: `http://localhost:5000`

### Method 2: Service NodePort (Testing)

```bash
kubectl get svc flask-app-service -n flask-app
```

### Method 3: Ingress (Production)

If using Ingress, access via the configured hostname.

## 📊 Kubernetes Resources Explained

### 🔧 Namespace (`namespace.yaml`)
- Isolates application resources
- Provides logical separation
- Enables resource quotas

### ⚙️ ConfigMap (`configmap.yaml`)
- Manages environment variables
- Separates configuration from code
- Supports hot-reloading for some configurations

### 💾 PersistentVolumeClaim (`persistentvolumeclaim.yaml`)
- Provides durable storage for SQLite database
- Retains data across pod restarts
- Uses dynamic provisioning

### 🚀 Deployment (`deployment.yaml`)
- Manages pod lifecycle
- Handles rolling updates
- Configures resource limits
- Sets up health checks
- Defines security context

### 🌐 Service (`service.yaml`)
- Provides stable network endpoint
- Load balances traffic
- Enables service discovery

### 🛣️ Ingress (`ingress.yaml`)
- Manages external HTTP/HTTPS access
- Provides SSL termination
- Enables path-based routing

## 🐛 Troubleshooting

### Common Issues and Solutions

1. **Image Pull Errors**
   ```bash
   kubectl describe pod -n flask-app
   ```

2. **Database Issues**
   ```bash
   kubectl exec -it deployment/flask-app -n flask-app -- ls -la /app/website/
   ```

3. **Service Access Problems**
   ```bash
   kubectl get endpoints -n flask-app
   ```

4. **Resource Constraints**
   ```bash
   kubectl top pods -n flask-app
   ```

## 🙏 Acknowledgments

- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
- [Flask Documentation](https://flask.palletsprojects.com/)
- [Docker Documentation](https://docs.docker.com/)

---


