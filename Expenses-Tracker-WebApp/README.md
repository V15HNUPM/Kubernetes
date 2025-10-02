```markdown
# 💰 Expenses Tracker WebApp - Spring Boot & Kubernetes

A full-stack Expenses Tracker application built with Spring Boot, MySQL, and deployed on Kubernetes with complete microservices architecture.

![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)

## 📋 About

This project demonstrates a production-ready expenses tracking application with:
- **Spring Boot** backend with REST APIs
- **MySQL** database for data persistence
- **Multi-stage Docker** build for optimized images
- **Kubernetes** orchestration with service discovery
- **Health checks** and monitoring endpoints

## 📁 Project Structure

```
Expenses-Tracker-WebApp/
├── k8s-manifests/              # Kubernetes configuration files
│   ├── namespace.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   ├── mysql-pvc.yaml
│   ├── mysql-deployment.yaml
│   ├── mysql-service.yaml
│   ├── app-deployment.yaml
│   ├── app-service.yaml
│   └── ingress.yaml
├── src/                        # Spring Boot source code
├── Dockerfile                  # Multi-stage Docker build
├── pom.xml                     # Maven dependencies
└── README.md                   # This file
```

## 🚀 Quick Start

### Prerequisites
- Docker
- Kubernetes cluster (Minikube, Kind, or cloud)
- kubectl
- Maven (for local development)

### 1. Build and Push Docker Image
```bash
docker build -t your-username/expenses-tracker:latest .
docker push your-username/expenses-tracker:latest
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
kubectl apply -f k8s-manifests/app-deployment.yaml
kubectl apply -f k8s-manifests/app-service.yaml
kubectl apply -f k8s-manifests/ingress.yaml
```

### 3. Access the Application
```bash
# Port forward to access the application
kubectl port-forward service/expenses-app-service 8080:80 -n springboot-expenses
```

Visit: http://localhost:8080

## 🔧 Kubernetes Architecture

### Services Deployed
- **Spring Boot App**: Java application running on port 8080
- **MySQL Database**: Persistent database service on port 3306
- **Service Discovery**: Internal DNS resolution between services

### Configuration
- **Namespace**: `springboot-expenses` for environment isolation
- **ConfigMap**: Application configuration and environment variables
- **Secret**: Sensitive data (database passwords)
- **Persistent Volume**: MySQL data persistence
- **Health Checks**: Spring Boot Actuator health endpoints

## 📊 Management Commands

```bash
# Check all resources
kubectl get all -n springboot-expenses

# View Spring Boot application logs
kubectl logs -f deployment/expenses-app -n springboot-expenses

# Check MySQL logs and database
kubectl logs deployment/mysql -n springboot-expenses
kubectl exec -it deployment/mysql -n springboot-expenses -- mysql -u root -pTest@123 -e "USE expenses_tracker; SHOW TABLES;"

# Restart deployment
kubectl rollout restart deployment/expenses-app -n springboot-expenses

# Scale application
kubectl scale deployment/expenses-app --replicas=3 -n springboot-expenses

# Delete everything
kubectl delete -f k8s-manifests/ -n springboot-expenses
```

## 🐳 Docker Details

The application uses a multi-stage Docker build:
- **Stage 1**: Maven with OpenJDK 17 for building
- **Stage 2**: OpenJDK 17 Alpine for runtime (smaller image)
- **Optimized**: Only JAR file copied to final image

## 🔍 Troubleshooting

### Common Issues
```bash
# Check pod status and events
kubectl get pods -n springboot-expenses
kubectl describe pod -n springboot-expenses

# Check service endpoints
kubectl get endpoints -n springboot-expenses

# Test database connection
kubectl run mysql-test -n springboot-expenses --image=mysql:latest --rm -it --restart=Never -- mysql -h mysql-service -u root -pTest@123 -e "SHOW DATABASES;"

# Test DNS resolution
kubectl run dns-test -n springboot-expenses --image=busybox --rm -it --restart=Never -- nslookup mysql-service
```

### Database Issues
If tables aren't created automatically:
```bash
kubectl exec -it deployment/mysql -n springboot-expenses -- mysql -u root -pTest@123 -e "USE expenses_tracker; SHOW TABLES;"
```

## 🛠️ Development

### Local Development
```bash
mvn spring-boot:run
```

### Environment Variables
- `SPRING_DATASOURCE_URL`: MySQL connection URL
- `SPRING_DATASOURCE_USERNAME`: Database username
- `SPRING_DATASOURCE_PASSWORD`: Database password
- `SPRING_PROFILES_ACTIVE`: Spring profiles (production/development)
- `SERVER_PORT`: Application port (8080)



## 🔗 Source

This project is based on: [https://github.com/LondheShubham153/Expenses-Tracker-WebApp](https://github.com/LondheShubham153/Expenses-Tracker-WebApp)

---

**Happy Expense Tracking!** 💰🚀
```
