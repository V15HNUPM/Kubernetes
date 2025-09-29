```markdown
# 🚀 Flask Application with Kubernetes Deployment

A simple Flask application containerized with Docker and deployed on Kubernetes.

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

## 📁 Project Structure

```
flask-app-ecs/
├── K8-manifests/          # Kubernetes configuration files
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   └── hpa.yaml
├── app.py                 # Flask application
├── run.py                 # Application entry point
├── requirements.txt       # Python dependencies
├── Dockerfile            # Multi-stage Docker build
└── README.md             # This file
```

## 🚀 Quick Start

### 1. Build and Push Docker Image

```bash
# Build the multi-stage Docker image
docker build -t your-username/flask-app:latest .

# Push to Docker Hub
docker push your-username/flask-app:latest
```

### 2. Update Image Reference

Edit `K8-manifests/deployment.yaml` and update the image name with your Docker Hub username.

### 3. Deploy to Kubernetes

```bash
# Apply all Kubernetes manifests
kubectl apply -f K8-manifests/namespace.yaml
kubectl apply -f K8-manifests/configmap.yaml
kubectl apply -f K8-manifests/deployment.yaml
kubectl apply -f K8-manifests/service.yaml
kubectl apply -f K8-manifests/ingress.yaml
kubectl apply -f K8-manifests/hpa.yaml
```

### 4. Access the Application

```bash
# Port forward to access the application
kubectl port-forward service/flask-app-service 8080:80 -n flask-app
```

Visit: http://localhost:8080

## 📋 Kubernetes Components

The deployment includes the following Kubernetes resources:

- **Namespace**: `flask-app` for environment isolation
- **ConfigMap**: Environment configuration for Flask app
- **Deployment**: Manages 3 replicas of the Flask application
- **Service**: Internal ClusterIP service on port 80
- **Ingress**: External access configuration
- **HPA**: Horizontal Pod Autoscaler (2-10 pods based on CPU)

## 🛠️ Management Commands

```bash
# Check deployment status
kubectl get all -n flask-app

# View application logs
kubectl logs deployment/flask-app -n flask-app -f

# Check pod status
kubectl get pods -n flask-app

# Monitor auto-scaling
kubectl get hpa -n flask-app

# Delete deployment
kubectl delete -f K8-manifests/ -n flask-app
```

## 🐛 Troubleshooting

### Common Issues

**Port forwarding fails:**
```bash
# Make sure Flask runs on 0.0.0.0, not 127.0.0.1
kubectl logs deployment/flask-app -n flask-app
```

**Check application status:**
```bash
kubectl describe pod -n flask-app
kubectl get events -n flask-app
```

**Debug container:**
```bash
kubectl exec -it deployment/flask-app -n flask-app -- /bin/sh
```

## 📝 Notes

- Update `your-username/flask-app:latest` with your actual Docker image
- Change `flask-app.local` in ingress to your domain
- Application runs on port 5000 inside container
- Service exposes it on port 80 internally

## 🔗 Source

This project is based on: [https://github.com/LondheShubham153/flask-app-ecs](https://github.com/LondheShubham153/flask-app-ecs)

---

```
