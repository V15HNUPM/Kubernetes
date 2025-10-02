# React Blog Kubernetes Deployment

This project deploys the StartBootstrap Clean Blog theme as a static website on Kubernetes.

## Source

- **Original Source**: [StartBootstrap Clean Blog](https://github.com/StartBootstrap/startbootstrap-clean-blog)
- **Docker Image**: `v15hnupm/react-blog:latest`

## Project Structure

```
k8s-manifests/
├── configmap.yaml          # Configuration data
├── deployment.yaml         # Application deployment
├── hpa.yaml               # Horizontal Pod Autoscaler
├── ingress.yaml           # Ingress configuration
├── namespace.yaml         # Kubernetes namespace
└── service.yaml           # Service configuration
```

## Prerequisites

- Kubernetes cluster
- `kubectl` configured
- Docker image built and pushed to registry

## Deployment

### 1. Create Namespace

```bash
kubectl apply -f namespace.yaml
```

### 2. Deploy Application Components

```bash
kubectl apply -f configmap.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f hpa.yaml
kubectl apply -f ingress.yaml
```

## Configuration Files

### namespace.yaml

```yaml
# Creates the react-blog namespace
```

### configmap.yaml

```yaml
# Contains configuration data for the application
```

### deployment.yaml

- **Namespace**: `react-blog`
- **Replicas**: 2
- **Image**: `v15hnupm/react-blog:latest`
- **Port**: 3000

### service.yaml

- **Type**: LoadBalancer
- **Service Port**: 80
- **Target Port**: 3000

### hpa.yaml

- Horizontal Pod Autoscaler configuration
- Automatically scales pods based on CPU utilization

### ingress.yaml

- Ingress configuration for external access
- URL routing rules

## Verification

### Check All Resources

```bash
kubectl get all -n react-blog
```

### Check Specific Resources

```bash
# Check pods
kubectl get pods -n react-blog

# Check services
kubectl get services -n react-blog

# Check ingress
kubectl get ingress -n react-blog

# Check HPA
kubectl get hpa -n react-blog

# Check configmaps
kubectl get configmaps -n react-blog
```

### Access Application

#### Method 1: Port Forwarding

```bash
kubectl port-forward service/react-service 8080:80 -n react-blog
```

Access: http://localhost:8080

#### Method 2: LoadBalancer (if supported by your cluster)

```bash
kubectl get service react-service -n react-blog
```

Use the external IP provided.

#### Method 3: Ingress (if configured)

```bash
kubectl get ingress -n react-blog
```

Use the ingress hostname or IP.

### View Logs

```bash
kubectl logs -n react-blog deployment/react-app
```

## Application Details

The application is a static blog website built with:

- **HTML/CSS/JavaScript**
- **Pug templates**
- **SASS/SCSS**
- **Bootstrap 5.2.3**

### Build Process

The application uses a custom build process:

```bash
npm run build  # Cleans, builds Pug, SCSS, scripts, and assets
npm start     # Builds and starts the development server
```

### Features

- Responsive design
- Blog post templates
- About and Contact pages
- Modern CSS with SASS

## Monitoring and Scaling

### Horizontal Pod Autoscaler

The HPA automatically scales the deployment based on CPU utilization:

- Minimum pods: 2
- Maximum pods: 10
- Target CPU utilization: 50%

### Check HPA Status

```bash
kubectl describe hpa -n react-blog
```

## Troubleshooting

### Common Issues

1. **Connection Refused**

   - Ensure service `targetPort` matches container port (3000)
   - Check pods are running: `kubectl get pods -n react-blog`

2. **Application Not Starting**

   - Check logs: `kubectl logs -n react-blog <pod-name>`
   - Verify build process completed successfully

3. **Image Pull Issues**

   - Ensure Docker image is publicly accessible
   - Check image tag matches deployment

4. **Ingress Not Working**
   - Verify ingress controller is installed
   - Check ingress configuration: `kubectl describe ingress -n react-blog`

### Debugging

```bash
# Debug pod
kubectl run debug-pod -n react-blog --image=v15hnupm/react-blog:latest --rm -it --restart=Never -- /bin/sh

# Check application files
ls -la dist/

# Test application startup
npm start

# Check configmap contents
kubectl describe configmap -n react-blog
```

## Maintenance

### Update Deployment

```bash
kubectl rollout restart deployment/react-app -n react-blog
```

### Scale Application Manually

```bash
kubectl scale deployment/react-app --replicas=3 -n react-blog
```

### Update Configuration

```bash
# Update configmap
kubectl apply -f configmap.yaml

# Restart pods to pick up new config
kubectl rollout restart deployment/react-app -n react-blog
```

### Cleanup

```bash
# Delete all resources
kubectl delete -f ./

# Delete namespace (includes all resources in the namespace)
kubectl delete namespace react-blog
```

## Architecture Overview

```
Internet
    │
    ▼
[ Ingress ]           # Routes external traffic
    │
    ▼
[ Service ]           # Load balances between pods
    │
    ▼
[ Pods ]              # Application instances (2-10 pods)
    │
    ▼
[ ConfigMap ]         # Application configuration
    │
    ▼
[ HPA ]              # Auto-scales based on load
```
