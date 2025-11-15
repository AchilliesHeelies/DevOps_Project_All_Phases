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
docker build -t flask-helllo-world .
```

### Run the container:
```bash
docker run -p 5000:5000 flask-helllo-world
```

### Or use Docker Compose:
```bash
docker compose up
```

## Docker Hub

Image available at: `vitalikergin/flask-helllo-world:v1.0`

Pull and run:
```bash
docker pull vitalikergin/flask-helllo-world:v1.0
docker run -p 5000:5000 vitalikergin/flask-helllo-world:v1.0
```
