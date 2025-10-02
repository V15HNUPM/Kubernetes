# DevOps Kubernetes Projects Collection

This repository contains a collection of Kubernetes-managed projects I've implemented as part of my DevOps journey. Each project demonstrates different aspects of container orchestration, deployment strategies, and cloud-native application management using Kubernetes.

## 🚀 Projects Overview

| Project Name | Description | Technology Stack | Application Type |
|-------------|-------------|-----------------|------------------|
| **BasicFlaskApplication** | Simple Flask web application | Python, Flask | Web Application |
| **django-notes-app** | Django-based notes application | Python, Django, SQLite | CRUD Application |
| **Expenses-Tracker-WebApp** | Web application for tracking expenses | Python, Flask, MySQL | Financial Application |
| **flask-app-ecs** | Flask application configured for container deployment | Python, Flask | Microservice |
| **node-express-mongodb** | Node.js Express application with MongoDB | Node.js, Express, MongoDB | Full Stack Application |
| **Python-Django-Blog-Website** | Blog website built with Django | Python, Django, PostgreSQL | Content Management |
| **simple-java-docker** | Java application with container configuration | Java, Spring Boot | Backend Service |
| **startbootstrap-clean-blog** | Clean blog template implementation | HTML, CSS, JavaScript | Static Website |
| **two-tier-flask-app** | Two-tier Flask application architecture | Python, Flask, MySQL | Multi-tier Application |

## 🏗️ Architecture

All projects follow cloud-native principles with:
- **Containerized Applications** using Docker
- **Kubernetes Orchestration** for deployment and scaling
- **Service Discovery** and load balancing
- **Persistent Storage** for stateful applications
- **Health Checks** and self-healing capabilities

## 📁 Repository Structure

```
devops-kubernetes-projects/
├── BasicFlaskApplication/
│   ├── k8s/
│   │   ├── deployment.yaml
│   │   └── service.yaml
│   └── README.md
├── django-notes-app/
│   ├── k8s/
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── pvc.yaml
│   └── README.md
├── Expenses-Tracker-WebApp/
│   ├── k8s/
│   │   ├── mysql/
│   │   └── flask-app/
│   └── README.md
├── flask-app-ecs/
│   └── k8s/
├── node-express-mongodb/
│   ├── k8s/
│   │   ├── backend/
│   │   └── database/
│   └── README.md
├── Python-Django-Blog-Website/
│   ├── k8s/
│   │   ├── django-app/
│   │   └── postgresql/
│   └── README.md
├── simple-java-docker/
│   └── k8s/
├── startbootstrap-clean-blog/
│   └── k8s/
├── two-tier-flask-app/
│   ├── k8s/
│   │   ├── namespace.yaml
│   │   ├── mysql-deployment.yaml
│   │   ├── mysql-service.yaml
│   │   ├── flask-deployment.yaml
│   │   └── flask-service.yaml
│   └── README.md
└── README.md
```

## 🛠️ Quick Start

### Prerequisites

- Kubernetes cluster (Minikube, Kind, or cloud provider)
- kubectl configured
- Docker (for building images)

### Deployment Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/devops-kubernetes-projects
   cd devops-kubernetes-projects
   ```

2. **Deploy a specific project**
   ```bash
   # Example: Deploy two-tier-flask-app
   kubectl apply -f two-tier-flask-app/k8s/
   
   # Check deployment status
   kubectl get all -n two-tier-app
   ```

3. **Access the application**
   ```bash
   # Port forward to access locally
   kubectl port-forward service/flask-app 5000:5000 -n two-tier-app
   # Visit http://localhost:5000
   ```

## 📊 Project Categories

### 🔄 Stateless Applications
- BasicFlaskApplication
- flask-app-ecs  
- startbootstrap-clean-blog
- simple-java-docker

### 💾 Stateful Applications
- django-notes-app (SQLite)
- node-express-mongodb (MongoDB)
- Python-Django-Blog-Website (PostgreSQL)

### 🏗️ Multi-tier Applications
- Expenses-Tracker-WebApp (Flask + MySQL)
- two-tier-flask-app (Flask + MySQL)

## 🎯 Learning Objectives

This repository demonstrates my proficiency in:

### Containerization
- Docker image creation and optimization
- Multi-stage builds
- Container security best practices

### Kubernetes Fundamentals
- Pods, Deployments, and Services
- ConfigMaps and Secrets
- Persistent Volumes and Claims
- Namespaces and resource isolation

### Application Deployment
- Rolling updates and rollbacks
- Health checks (liveness & readiness probes)
- Resource limits and requests
- Service discovery and load balancing

### DevOps Practices
- Infrastructure as Code (IaC)
- GitOps workflow principles
- Continuous Deployment strategies
- Monitoring and logging setup

## 🔧 Common Kubernetes Patterns Demonstrated

1. **Web Application Deployment** - Flask, Django, Node.js apps
2. **Database Backends** - MySQL, MongoDB, PostgreSQL
3. **Multi-container Pods** - App + sidecar patterns
4. **Service Mesh Ready** - Proper service naming and discovery
5. **Health Monitoring** - Comprehensive probe configurations

## 📈 Monitoring & Management

```bash
# Check overall cluster status
kubectl get nodes
kubectl cluster-info

# Monitor specific project
kubectl get pods,svc,deploy -l app=your-app-name

# View logs
kubectl logs -f deployment/your-deployment

# Resource usage
kubectl top pods
```

## 🧹 Cleanup

```bash
# Delete all resources for a project
kubectl delete -f project-name/k8s/

# Or delete by namespace (if applicable)
kubectl delete namespace project-namespace
```

## 🤝 Contributing

This is a learning repository showcasing my DevOps journey. While primarily for demonstration purposes, suggestions and improvements are welcome!

## 📚 Resources

- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
- [Kubernetes Patterns](https://kubernetes.io/docs/concepts/configuration/overview/)
- [Docker Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

## 📄 License

This collection is for educational and demonstration purposes. Each project maintains its original license from the source repositories.

---

**Note**: This repository represents my hands-on learning experience with Kubernetes and cloud-native technologies. Each project has been adapted and configured for Kubernetes deployment while maintaining the original application functionality.
