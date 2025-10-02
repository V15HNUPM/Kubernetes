```markdown
# 🐍 Django Notes App with MySQL & Kubernetes

A full-stack Django application with MySQL database, containerized with Docker and deployed on Kubernetes with Nginx as a reverse proxy.

![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)

## 📋 About

This project demonstrates a production-ready Django application with:
- **Django** web framework with Gunicorn WSGI server
- **MySQL** database for data persistence
- **Nginx** as reverse proxy and static file server
- **Docker** containerization
- **Kubernetes** orchestration with multi-service deployment

## 📁 Project Structure

```
django-notes-app/
├── k8s-manifests/              # Kubernetes configuration files
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── mysql-deployment.yaml
│   ├── mysql-service.yaml
│   ├── django-deployment.yaml
│   ├── django-service.yaml
│   ├── nginx-deployment.yaml
│   ├── nginx-service.yaml
│   └── nginx-configmap.yaml
├── notesapp/                   # Django project
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── Dockerfile                  # Multi-stage Docker build
├── requirements.txt            # Python dependencies
├── manage.py                   # Django management script
└── README.md                   # This file
```

## 🚀 Quick Start

### Prerequisites
- Docker
- Kubernetes cluster (Minikube, Kind, or cloud)
- kubectl

### 1. Build and Push Docker Image
```bash
docker build -t your-username/django-notes-app:latest .
docker push your-username/django-notes-app:latest
```

### 2. Deploy to Kubernetes
```bash
# Apply all Kubernetes manifests
kubectl apply -f k8s-manifests/namespace.yaml
kubectl apply -f k8s-manifests/configmap.yaml
kubectl apply -f k8s-manifests/mysql-deployment.yaml
kubectl apply -f k8s-manifests/mysql-service.yaml
kubectl apply -f k8s-manifests/django-deployment.yaml
kubectl apply -f k8s-manifests/django-service.yaml
kubectl apply -f k8s-manifests/nginx-configmap.yaml
kubectl apply -f k8s-manifests/nginx-deployment.yaml
kubectl apply -f k8s-manifests/nginx-service.yaml
```

### 3. Access the Application
```bash
# Port forward to access the application
kubectl port-forward service/nginx-service 8080:80 -n django-notes-app
```

Visit: http://localhost:8080

## 🔧 Kubernetes Architecture

### Services Deployed
- **Django App**: Python application running on port 8000 with Gunicorn
- **MySQL**: Database service on port 3306 with persistent storage
- **Nginx**: Web server and reverse proxy on port 80
- **Internal Networking**: Services communicate via ClusterIP

### Configuration
- **Namespace**: `django-notes-app` for environment isolation
- **ConfigMap**: Environment variables and Nginx configuration
- **Deployments**: Managed pod lifecycle with health checks
- **Services**: Internal service discovery and load balancing
- **Persistent Volume**: MySQL data persistence

## 📊 Management Commands

```bash
# Check all resources
kubectl get all -n django-notes-app

# View Django application logs
kubectl logs deployment/django -n django-notes-app -f

# Check MySQL logs
kubectl logs deployment/mysql -n django-notes-app

# Check Nginx logs
kubectl logs deployment/nginx -n django-notes-app

# Run Django management commands
kubectl exec -it deployment/django -n django-notes-app -- python manage.py migrate
kubectl exec -it deployment/django -n django-notes-app -- python manage.py createsuperuser

# Restart deployment
kubectl rollout restart deployment/django -n django-notes-app

# Delete everything
kubectl delete -f k8s-manifests/ -n django-notes-app
```

## 🐳 Docker Details

The application uses an optimized Docker setup:
- **Python 3.9** base image
- **MySQL client** dependencies installed
- **Gunicorn** as production WSGI server
- **Multi-service** architecture

## 🔍 Troubleshooting

### Common Issues
```bash
# Check pod status and events
kubectl get pods -n django-notes-app
kubectl describe pod -n django-notes-app

# Check service endpoints
kubectl get endpoints -n django-notes-app

# Debug database connection
kubectl exec -it deployment/mysql -n django-notes-app -- mysql -u root -proot -e "SHOW DATABASES;"
```

### Database Migrations
If migrations weren't applied during deployment:
```bash
kubectl exec -it deployment/django -n django-notes-app -- python manage.py migrate
```


## 🔗 Source

This project is based on: [https://github.com/LondheShubham153/django-notes-app](https://github.com/LondheShubham153/django-notes-app)

**Happy Coding!** 🚀
```
