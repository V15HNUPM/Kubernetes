# Two-Tier Flask MySQL Application

A two-tier web application built with Flask and MySQL, containerized with Docker and deployed on Kubernetes.

## 📋 Project Overview

This project demonstrates a two-tier architecture with:
- **Frontend**: Flask web application
- **Backend**: MySQL database
- **Containerization**: Docker
- **Orchestration**: Kubernetes

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐
│   Flask App     │    │   MySQL         │
│   (Python)      │    │   Database      │
│   Port: 5000    │    │   Port: 3306    │
└─────────────────┘    └─────────────────┘
         │                      │
         └──────────────────────┘
                 Kubernetes
```

## 📁 Project Structure

```
two-tier-flask-app/
├── Dockerfile
├── requirements.txt
├── app.py
├── k8s/
│   ├── namespace.yaml
│   ├── mysql-pvc.yaml
│   ├── mysql-deployment.yaml
│   ├── mysql-service.yaml
│   ├── flask-deployment.yaml
│   └── flask-service.yaml
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- Docker
- Kubernetes cluster (Minikube, Docker Desktop, or cloud provider)
- kubectl

### 1. Clone the Repository

```bash
git clone https://github.com/LondheShubham153/two-tier-flask-app
cd two-tier-flask-app
```

### 2. Build Docker Image

```bash
docker build -t your-username/two-tier-flask-app:latest .
```

### 3. Deploy to Kubernetes

```bash
# Apply all Kubernetes manifests
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/mysql-pvc.yaml
kubectl apply -f k8s/mysql-deployment.yaml
kubectl apply -f k8s/mysql-service.yaml
kubectl apply -f k8s/flask-deployment.yaml
kubectl apply -f k8s/flask-service.yaml
```

### 4. Check Deployment Status

```bash
kubectl get all -n two-tier-app
```

### 5. Access the Application

```bash
kubectl port-forward -n two-tier-app service/flask-app 5000:5000
```
Then visit: `http://localhost:5000`

## 🔧 Kubernetes Manifests

The application is deployed using the following Kubernetes resources:

- **Namespace**: `two-tier-app` for isolation
- **MySQL**: 
  - Deployment with persistent volume claim (5GB)
  - Headless service for database connectivity
- **Flask App**:
  - Deployment with 2 replicas
  - LoadBalancer/NodePort service for external access


## 🛠️ Development

### Local Development with Docker Compose

```bash
docker-compose up
```

### Running Tests

```bash
# Test database connection
curl http://localhost:5000/health

# Test user creation
curl -X POST http://localhost:5000/users -H "Content-Type: application/json" -d '{"name":"John","email":"john@example.com"}'

# Test listing users
curl http://localhost:5000/users
```

## 📊 Monitoring

Check application status:

```bash
# Check pods
kubectl get pods -n two-tier-app

# Check services
kubectl get services -n two-tier-app

# View logs
kubectl logs -n two-tier-app -l app=flask-app

# Check persistent volumes
kubectl get pvc -n two-tier-app
```

## 🧹 Cleanup

To remove the application from Kubernetes:

```bash
kubectl delete -f k8s/ --recursive
```

Or delete the namespace (this will remove all resources):

```bash
kubectl delete namespace two-tier-app
```

## 🔐 Environment Variables

The application uses the following environment variables:

- `MYSQL_HOST`: MySQL hostname (default: mysql)
- `MYSQL_USER`: MySQL username (default: root)
- `MYSQL_PASSWORD`: MySQL password (default: root)
- `MYSQL_DB`: MySQL database name (default: devops)

## 🙏 Acknowledgments

Based on the original work from [LondheShubham153/two-tier-flask-app](https://github.com/LondheShubham153/two-tier-flask-app)

---

**Note**: Remember to replace `your-username` with your actual Docker Hub username when building and pushing the image.
