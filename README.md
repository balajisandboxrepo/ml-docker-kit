# ml‑docker‑kit

![GitHub Repo stars](https://img.shields.io/github/stars/yourusername/ml-docker-kit?style=social)
![Docker Pulls](https://img.shields.io/docker/pulls/yourusername/ml-docker-kit)

## 📖 Overview

`ml-docker-kit` is a **starter template** for serving a machine‑learning model via a FastAPI web service inside a Docker container. It demonstrates how to:
- Load a pre‑trained scikit‑learn model and scaler.
- Expose a **RESTful prediction API**.
- Package the whole stack into a reproducible Docker image.

## 🏗️ System Architecture

```mermaid
flowchart TD
    subgraph Container[Docker Container]
        direction LR
        FastAPI[FastAPI App (uvicorn)] --> Model[model.pkl]
        FastAPI --> Scaler[scaler.pkl]
        FastAPI --> API[HTTP Endpoints]
    end
    Client[Client] -->|HTTP Request| API
    API -->|Prediction| Model
    Model -->|Scaled Input| Scaler
```

*The container bundles the Python runtime, model artifacts, and the FastAPI service. Clients interact over HTTP.*

## 🚀 Getting Started

### Prerequisites
- Docker Engine (>= 24)
- Optional: Python 3.11+ (for local development)

### Build the Docker Image
```bash
docker build -t ml-docker-kit:latest .
```

### Run the Container
```bash
docker run -d -p 8000:8000 --name ml-docker-kit ml-docker-kit:latest
```
The API will be available at `http://localhost:8000`.

### Test the API
```bash
curl -X POST "http://localhost:8000/predict" \
     -H "Content-Type: application/json" \
     -d '{
           "alcohol": 13.2,
           "malic_acid": 2.77,
           "ash": 2.51,
           "alcalinity_of_ash": 18.5,
           "magnesium": 96,
           "total_phenols": 2.45,
           "flavanoids": 2.53,
           "nonflavanoid_phenols": 0.29,
           "proanthocyanins": 1.54,
           "color_intensity": 5.0,
           "hue": 1.04,
           "od280_od315_of_diluted_wines": 3.47,
           "proline": 920
         }'