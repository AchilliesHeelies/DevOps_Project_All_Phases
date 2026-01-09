# Flask Hello World - DevOps Project Phase 1

A simple Flask application containerized with Docker.

## Prerequisites
- Docker installed
- Docker Hub account

## Running Locally (Native Python)

1. Create virtual environment:
```bash
python3 -m venv venv
source venv/bin/activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the application:
```bash
python3 app.py
```

Visit: http://127.0.0.1:5000

## Running with Docker

### Build the image:
```bash
docker build -t flask-hello-world .
```

### Run the container:
```bash
docker run -p 5000:5000 flask-hello-world
```

### Or use Docker Compose:
```bash
docker compose up
```

## Docker Hub

Image available at: `vitalikergin/flask-hello-world:latest`

Pull and run:
```bash
docker pull vitalikergin/flask-hello-world:latest
docker run -p 5000:5000 vitalikergin/flask-hello-world:latest
```
## Phase 2: Kubernetes Deployment with Helm

The application is deployed to Kubernetes using Helm charts.

### Features:
- Horizontal Pod Autoscaling (2-5 replicas, 50% CPU target)
- ConfigMap for environment configuration
- Liveness and Readiness probes
- Resource requests and limits
- NodePort service for external access

### Deployment:
```bash
cd kubernetes/flask-app
helm install flask-app .
```

### Access:
```bash
minikube service flask-app --url
```

See `kubernetes/flask-app/README.md` for detailed Helm chart documentation.

## Phase 3: Automation with Jenkins CI/CD

Implemented automated deployment pipeline using Jenkins.

### Pipeline Stages:
1. **Checkout** - Pull latest code from Git
2. **Build** - Build Docker image
3. **Test** - Validate image creation
4. **Deploy** - Deploy to Kubernetes using Helm

### Running the Pipeline:
The pipeline automatically triggers on code changes and deploys the Flask application to Minikube.

Docker image: `vitalikergin/flask-hello-world:latest`

### Features:
- Automated Docker image builds
- Kubernetes deployment via Helm

Repository: https://github.com/AchilliesHeelies/DevOps_Project_1
