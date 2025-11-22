# Flask App Helm Chart - Phase 2

Kubernetes deployment of the Flask "Hello World" application using Helm.

## Features

- **Deployment**: Flask application with configurable replicas
- **Service**: NodePort service exposing port 5000
- **Horizontal Pod Autoscaler (HPA)**: Auto-scales between 2-5 pods based on 50% CPU utilization
- **ConfigMap**: Environment-specific configuration (ENVIRONMENT, APP_NAME, LOG_LEVEL)
- **Health Probes**:
  - Liveness Probe: HTTP check on `/` (10s delay, 5s period)
  - Readiness Probe: HTTP check on `/` (5s delay, 3s period)
- **Resource Management**: CPU and memory requests/limits configured

## Prerequisites

- Kubernetes cluster (Minikube for local development)
- Helm 3.x installed
- Docker image: `vitalikergin/flask-helllo-world:v1.0`

## Installation

### Deploy the chart:
```# Flask App Helm Chart - Phase 2

Kubernetes deployment of the Flask "Hello World" application using Helm.

## Features

- **Deployment**: Flask application with configurable replicas
- **Service**: NodePort service exposing port 5000
- **Horizontal Pod Autoscaler (HPA)**: Auto-scales between 2-5 pods based on 50% CPU utilization
- **ConfigMap**: Environment-specific configuration (ENVIRONMENT, APP_NAME, LOG_LEVEL)
- **Health Probes**:
  - Liveness Probe: HTTP check on `/` (10s delay, 5s period)
  - Readiness Probe: HTTP check on `/` (5s delay, 3s period)
- **Resource Management**: CPU and memory requests/limits configured

## Prerequisites

- Kubernetes cluster (Minikube for local development)
- Helm 3.x installed
- Docker image: `vitalikergin/flask-helllo-world:v1.0`

## Installation

### Deploy the chart:
```bash
helm install flask-app .
```

### Verify deployment:
```bash
kubectl get all
kubectl get hpa
kubectl get configmap
```

### Access the application:
```bash
minikube service flask-app --url
```

## Configuration

Key values in `values.yaml`:

- `image.repository`: Docker image repository
- `image.tag`: Image version
- `service.type`: Service type (NodePort for local access)
- `service.port`: Application port (5000)
- `autoscaling.enabled`: Enable HPA
- `autoscaling.minReplicas`: Minimum pod count (2)
- `autoscaling.maxReplicas`: Maximum pod count (5)
- `autoscaling.targetCPUUtilizationPercentage`: Target CPU for scaling (50%)
- `resources.requests`: Resource requests (CPU: 100m, Memory: 128Mi)
- `resources.limits`: Resource limits (CPU: 200m, Memory: 256Mi)

## Upgrading
```bash
# Modify values.yaml, then:
helm upgrade flask-app .
```

## Uninstalling
```bash
helm uninstall flask-app
```

## Testing HPA

Generate load to test autoscaling:
```bash
kubectl run load-generator --image=busybox --restart=Never -- /bin/sh -c "while true; do wget -q -O- http://flask-app:5000; done"

# Watch HPA scale up:
kubectl get hpa -w

# Stop load generator:
kubectl delete pod load-generator
```
