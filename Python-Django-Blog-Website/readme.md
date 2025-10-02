```markdown
# 🐍 Django Blog Website with MySQL & Kubernetes

A full-featured Django blog application with MySQL database, containerized with Docker and deployed on Kubernetes.

![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

## 📋 About

This project demonstrates a production-ready Django blog application with:
- **Django** web framework with built-in admin interface
- **MySQL** database for data persistence
- **Docker** containerization with optimized Python image
- **Kubernetes** orchestration with service discovery
- **Blog features** including posts, categories, and user authentication

## 📁 Project Structure

```
Python-Django-Blog-Website/
├── k8s-manifests/              # Kubernetes configuration files
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   ├── mysql-pvc.yaml
│   ├── mysql-deployment.yaml
│   ├── mysql-service.yaml
│   ├── django-deployment.yaml
│   ├── django-service.yaml
│   └── ingress.yaml
├── blog/                       # Django project
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── blogapp/                # Django app
├── Dockerfile                  # Python 3.11 with MySQL client
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
docker build -t your-username/django-blog:latest .
docker push your-username/django-blog:latest
```

### 2. Deploy to Kubernetes
```bash
# Apply all Kubernetes manifests in order
kubectl apply -f k8s-manifests/namespace.yaml
kubectl apply -f k8s-manifests/configmap.yaml
kubectl apply -f k8s-manifests/secret.yaml
kubectl apply -f k8s-manifests/mysql-pvc.yaml
kubectl apply -f k8s-manifests/mysql-deployment.yaml
kubectl apply -f k8s-manifests/mysql-service.yaml
kubectl apply -f k8s-manifests/django-deployment.yaml
kubectl apply -f k8s-manifests/django-service.yaml
kubectl apply -f k8s-manifests/ingress.yaml
```

### 3. Access the Application
```bash
# Port forward to access the application
kubectl port-forward service/django-service 8080:80 -n django-blog
```

Visit: http://localhost:8080

## 🔧 Kubernetes Architecture

### Services Deployed
- **Django App**: Python application running on port 8000
- **MySQL Database**: Persistent database service on port 3306
- **Service Discovery**: Internal DNS resolution between services

### Configuration
- **Namespace**: `django-blog` for environment isolation
- **ConfigMap**: Django configuration and environment variables
- **Secret**: Database credentials and Django secret key
- **Persistent Volume**: MySQL data persistence
- **Resource Management**: Optimized CPU and memory limits

## 📊 Management Commands

```bash
# Check all resources
kubectl get all -n django-blog

# View Django application logs
kubectl logs -f deployment/django-app -n django-blog

# Check MySQL logs and database
kubectl logs deployment/mysql -n django-blog
kubectl exec -it deployment/mysql -n django-blog -- mysql -u root -prootpassword -e "SHOW DATABASES; USE blogdb; SHOW TABLES;"

# Run Django management commands
kubectl exec -it deployment/django-app -n django-blog -- python manage.py createsuperuser

# Restart deployment
kubectl rollout restart deployment/django-app -n django-blog

# Scale application
kubectl scale deployment/django-app --replicas=2 -n django-blog

# Delete everything
kubectl delete -f k8s-manifests/ -n django-blog
```

## 🌐 Application Features

- ✅ User authentication and authorization
- ✅ Blog post creation, editing, and deletion
- ✅ Categories and tags for posts
- ✅ Django admin interface
- ✅ MySQL database integration
- ✅ Responsive web design
- ✅ Comment system (if implemented)
- ✅ Search functionality

## 🐳 Docker Details

The application uses an optimized Docker setup:
- **Python 3.11** base image
- **MySQL client** dependencies installed
- **Development server** for testing (replace with Gunicorn for production)
- **Multi-stage build** ready for optimization

## 🔍 Troubleshooting

### Common Issues
```bash
# Check pod status and events
kubectl get pods -n django-blog
kubectl describe pod -n django-blog

# Check service endpoints
kubectl get endpoints -n django-blog

# Test database connection
kubectl run mysql-test -n django-blog --image=mysql:8.0 --rm -it --restart=Never -- mysql -h mysql-service -u bloguser -pblogpassword -e "SHOW DATABASES;"

# Test DNS resolution
kubectl run dns-test -n django-blog --image=busybox --rm -it --restart=Never -- nslookup mysql-service
```

### Database Migrations
If migrations fail during deployment:
```bash
kubectl exec -it deployment/django-app -n django-blog -- python manage.py makemigrations
kubectl exec -it deployment/django-app -n django-blog -- python manage.py migrate
```

## 🛠️ Development

### Local Development
```bash
python manage.py runserver
```

### Environment Variables
- `MYSQL_HOST`: MySQL service host (mysql-service)
- `MYSQL_DATABASE`: Database name (blogdb)
- `MYSQL_USER`: Database username (bloguser)
- `MYSQL_PASSWORD`: Database password (blogpassword)
- `MYSQL_PORT`: Database port (3306)
- `DEBUG`: Django debug mode (0 for production)
- `DJANGO_SETTINGS_MODULE`: Django settings module
- `ALLOWED_HOSTS`: Allowed hosts for Django


## 🔗 Source

This project is based on: [https://github.com/keerti1924/Python-Django-Blog-Website/tree/main](https://github.com/keerti1924/Python-Django-Blog-Website/tree/main)

---

**Happy Blogging!** ✍️🚀
```
