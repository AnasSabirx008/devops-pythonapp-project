# devops-pythonapp-project

A minimal Flask API packaged with Docker and deployed to Kubernetes, both with raw manifests and with a Helm chart.

## Stack
Python 3.13 · Flask · Docker · Kubernetes · Helm · Gateway API (HTTPRoute)

## Structure
```
src/app.py                       Flask API
Dockerfile                       Container image (python:3.13-slim)
infra/k8s-manifest/              Deployment, Service, HTTPRoute
infra/helm-charts/python-app/    Helm chart (deployment, service, ingress, httproute, SA)
```

## API
| Endpoint | Description |
|---|---|
| `GET /api/v1/info` | Time, pod hostname, environment |
| `GET /api/v1/healthz` | Health check |

## Run
```bash
# Local
docker build -t python-app .
docker run -p 5000:5000 python-app
curl localhost:5000/api/v1/info

# Kubernetes (raw manifests)
kubectl apply -f infra/k8s-manifest/

# Kubernetes (Helm)
helm install python-app infra/helm-charts/python-app
```
The Service exposes port `8080` → container port `5000`.
